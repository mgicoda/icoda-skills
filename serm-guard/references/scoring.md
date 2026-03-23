# SERM Guard — Scoring Reference

Exact scoring methodology for the Sentiment & Reputation Guard audit.

---

## Overall Reputation Score (0–100)

```
overall_score = round(
  search_sentiment_score  × 0.35 +
  serp_control_score      × 0.20 +
  platform_presence_score × 0.15 +
  llm_sentiment_score     × 0.30
)
```

**Weight rationale:**
- Search Sentiment (35%): the most direct measure of what people actually say
- LLM Sentiment (30%): increasingly critical as users ask AI about brands
- SERP Control (20%): measures the brand's ability to shape its own narrative
- Platform Presence (15%): measures coverage breadth across key review ecosystems

### Score Interpretation

| Range | Label | Hex Color | Text Color |
|-------|-------|-----------|------------|
| 80–100 | Strong reputation | `#22c55e` (green) | `#16a34a` |
| 65–79 | Good with gaps | `#eab308` (yellow) | `#ca8a04` |
| 50–64 | Needs attention | `#f97316` (orange) | `#ea580c` |
| 0–49 | At risk | `#ef4444` (red) | `#dc2626` |

---

## 1. Search Sentiment Score (0–100)

Measures the overall sentiment of search results across all queries.

### Sentiment Classification

| Sentiment | Raw Score | When to assign |
|-----------|-----------|----------------|
| Positive | 100 | Title/snippet clearly praises brand, recommends it, highlights strengths |
| Neutral | 60 | Informational, factual, directory listing, no clear positive or negative signal |
| Mixed | 40 | Contains both positive and negative signals in the same result |
| Negative | 0 | Title/snippet contains complaints, warnings, scam allegations, or clearly negative language |

**Rules:**
- Classify from title + snippet text ONLY. Do not fetch or quote the full page content.
- When ambiguous, default to **Neutral**. Be conservative with Positive and Negative.
- Brand's own content (company website, official blog) should still be classified by sentiment of the *content visible in the snippet*, but it's usually Positive or Neutral.

### Weighting Factors

**Position weight** — results higher on the page matter more:
```
position_weight = (11 - position) / 10

Position 1  → 1.0
Position 2  → 0.9
Position 3  → 0.8
...
Position 10 → 0.1
```

**Authority multiplier** — authoritative sources carry more weight:

| Authority Level | Multiplier | Examples |
|----------------|------------|----------|
| High | 1.5 | Major news outlets (BBC, Forbes, TechCrunch), Wikipedia, government sites, industry leaders (G2, Trustpilot, CoinGecko) |
| Medium | 1.0 | Industry-specific sites, established blogs, review platforms, social media platforms |
| Low | 0.5 | Unknown blogs, personal sites, low-traffic forums, spam-looking domains |

### Calculation

For each unique result (de-duplicated by URL, keeping highest position):

```
weighted_score = raw_sentiment × position_weight × authority_multiplier
max_possible   = 100 × position_weight × authority_multiplier
```

Final score:

```
search_sentiment_score = round( sum(weighted_score) / sum(max_possible) × 100 )
```

### Edge Cases

- **Fewer than 5 total results**: add a "Low confidence" flag to the report. Still compute the score.
- **De-duplication**: if the same URL appears in multiple queries (e.g., a Reddit thread appears for both "reviews" and "complaints"), count it only once using its best (lowest number) position.
- **No data queries**: queries that returned zero results are excluded from the calculation entirely.

---

## 2. SERP Control Rate (0–100)

Measures how much of the first search results page the brand controls or positively influences.

### Control Classification

For each result on the first page of the `"{brand}" reviews` query (or `"{brand}"` if the brand name is distinctive enough):

| Control Level | Weight | Definition |
|--------------|--------|------------|
| Owned | 1.0 | Brand's own website, official social media profiles, brand-controlled blogs |
| Earned Positive | 0.7 | Third-party content with clearly positive sentiment toward the brand |
| Earned Neutral | 0.3 | Third-party content that is factual/neutral — directories, Wikipedia, news without sentiment |
| Hostile | 0.0 | Negative reviews, complaint threads, competitor comparison pages positioning brand negatively |

### Calculation

```
raw_control = (count_owned × 1.0 + count_earned_positive × 0.7 + count_earned_neutral × 0.3 + count_hostile × 0.0) / total_results

serp_control_score = round(raw_control × 100)
```

**Position 1 bonus**: if the brand's own website occupies position 1, add +10 (capped at 100).

### Examples

| Scenario | Score |
|----------|-------|
| 10 results: 3 owned + 4 earned_positive + 2 neutral + 1 hostile | (3×1.0 + 4×0.7 + 2×0.3 + 1×0.0)/10 = 0.64 → 64 |
| 10 results: 1 owned (pos 1) + 2 earned_positive + 5 neutral + 2 hostile | (1+1.4+1.5+0)/10 = 0.39 → 39 + 10 (pos 1 bonus) = 49 |
| 10 results: 5 owned + 5 earned_positive | (5+3.5)/10 = 0.85 → 85 |

---

## 3. Platform Presence Score (0–100)

Measures how broadly the brand is represented across key review and discussion platforms.

### Platform Points

| Platform | Points | Detection |
|----------|--------|-----------|
| Review platform profile (Trustpilot, G2, Capterra, or niche equivalent) | +20 | Any result from trustpilot.com, g2.com, capterra.com, or niche review site |
| Google Business Profile | +20 | Google Maps/Business result in search, or `site:google.com/maps "{brand}"` |
| Reddit — substantive mentions | +20 | Results from reddit.com with actual discussion (not just a mention in passing) |
| YouTube — reviews or mentions | +20 | Results from youtube.com with brand-related video content |
| Quora — answers mentioning brand | +10 | Results from quora.com mentioning the brand |
| Glassdoor — employer presence | +10 | Results from glassdoor.com with company profile |

**Maximum: 100** (cap if sum exceeds 100)

### Detection Rules

- A platform is "found" if at least one result from that platform's domain appeared in ANY query's results.
- For Reddit: only count if the result appears to be a substantive discussion (thread with comments), not just a random mention.
- For YouTube: only count if the video title/snippet references the brand specifically.
- Niche review platforms count toward the "Review platform" slot:
  - Crypto: CoinGecko, CoinMarketCap, DeFiLlama
  - iGaming: AskGamblers, Casino.org, Casino Guru
  - SaaS: G2, Capterra, TrustRadius
  - Agency: Clutch.co, DesignRush, GoodFirms
  - Healthcare: Healthgrades, Vitals, WebMD
  - Legal: Avvo, Martindale-Hubbell
  - Travel: TripAdvisor, Booking.com reviews

---

## 4. LLM Sentiment Score (0–100)

Assesses how AI language models would likely perceive and present the brand based on available online signals.

### Base Score

Start at **50** (neutral baseline — brand exists but has no strong signals either way).

### Trust Signals (add up to +30)

| Signal | Points | Detection |
|--------|--------|-----------|
| Wikipedia page exists | +10 | Any result from en.wikipedia.org (or localized Wikipedia) mentioning the brand |
| Press coverage in major outlets | +5 each (max +15) | Results from top-tier news: Forbes, TechCrunch, Bloomberg, Reuters, BBC, NYT, Wired, The Verge, etc. |
| Regulatory/compliance mentions | +5 | Mentions of being licensed, regulated, compliant with industry standards |

### E-E-A-T Indicators (add up to +30)

| Signal | Points | Detection |
|--------|--------|-----------|
| Brand publishes expertise content | +10 | Blog, resource center, guides, whitepapers found in results |
| Experience proof (case studies, testimonials) | +10 | Case studies, client testimonials, portfolio found in results |
| Authoritative mentions from high-DR sources | +10 | Brand mentioned/linked by authoritative industry sites or publications |

### Red Flags (subtract up to -40)

| Signal | Penalty | Detection |
|--------|---------|-----------|
| "Scam" in top-5 results for brand query | -15 | Result with "scam", "fraud", "ponzi" in title appears in positions 1-5 |
| Unresolved complaint threads | -10 | Active complaint threads without brand response on review sites or forums |
| Legal issues mentioned | -10 | Lawsuits, regulatory actions, fines mentioned in results |
| Deceptive practices flagged | -5 | Hidden fees, misleading claims, fake reviews allegations in results |

### Content Quality (add up to +20)

| Signal | Points | Detection |
|--------|--------|-----------|
| Educational/substantive content | +10 | Brand produces how-to guides, tutorials, industry analysis |
| Structured data on website | +5 | Schema.org markup detected (Organization, Product, FAQPage) — note this from URL structure or snippet indicators |
| Active blog / resource center | +5 | Regular content publication visible in results (dated recent articles) |

### Final Calculation

```
llm_sentiment_score = clamp(
  50 + trust_signals + eeat + content_quality - red_flags,
  0, 100
)
```

### LLM Perception Labels

| Score Range | Label | Meaning |
|------------|-------|---------|
| 80–100 | Favorable | LLM would confidently recommend the brand |
| 60–79 | Positive-leaning | LLM would mention the brand positively with minor caveats |
| 40–59 | Neutral | LLM would present the brand factually without strong recommendation |
| 20–39 | Cautionary | LLM would include warnings or suggest alternatives |
| 0–19 | Negative | LLM would actively warn against the brand or refuse to recommend |

---

## Edge Cases & Special Rules

1. **Zero results across all queries**: Do not produce a numeric score. Output: "Score unavailable — brand has no detectable online presence. This itself is a significant finding."

2. **Very new brand** (<5 total results): Compute scores but add "Low data confidence" qualifier. Platform Presence and SERP Control will naturally score low, which is accurate.

3. **Only negative results**: Do NOT artificially inflate any component. A brand with only negative mentions deserves a low score — report it honestly.

4. **Comparison mode**: Each brand is scored 100% independently. Compare side-by-side only after individual scores are computed. Never let one brand's data influence the other's score.

5. **Ambiguous sentiment**: When a result could be either neutral or slightly positive/negative, always classify as **Neutral**. The scoring formula already accounts for position and authority — conservative classification prevents score inflation/deflation from uncertain data.
