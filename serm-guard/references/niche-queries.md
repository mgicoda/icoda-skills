# SERM Guard — Query Matrix by Niche

Complete query catalog for the Sentiment & Reputation Guard audit. Queries are grouped
into three tiers: Base (always run), Platform (always run), and Niche-Specific (based
on auto-detected industry).

---

## Niche Detection Heuristics

After the initial `WebSearch` for `"{brand}" company`, scan the top-5 result titles and
snippets for keyword signals. Assign the **first matching** niche:

| Keywords in results | Niche |
|---|---|
| blockchain, token, DeFi, crypto, wallet, NFT, coin, mining, staking, web3, DAO | `crypto` |
| casino, betting, slots, gambling, poker, sportsbook, wagering, jackpot, roulette | `igaming` |
| software, SaaS, platform, API, subscription, cloud, dashboard, integration, B2B tool | `saas` |
| agency, marketing agency, consulting, digital agency, creative agency, PR firm | `agency` |
| shop, store, buy, shipping, ecommerce, retail, products, marketplace, cart | `ecommerce` |
| fintech, banking app, payment, lending, neobank, investment platform, trading app | `fintech` |
| hospital, clinic, healthcare, medical, patient, doctor, pharmacy, telehealth | `healthcare` |
| law firm, attorney, lawyer, legal services, litigation, counsel | `legal` |
| real estate, property, realtor, broker, homes for sale, apartment, rental | `real_estate` |
| travel, hotel, airline, tourism, booking, vacation, resort, flights | `travel` |
| university, college, online course, education, academy, degree, certification, e-learning | `education` |
| *(none of the above)* | `general` |

If multiple niches match, prefer the one with the most keyword hits. If tied, prefer the
niche listed earlier in the table. Always tell the user the detected niche and allow correction.

---

## Base Queries (always run — 8 queries)

These queries cover universal reputation signals applicable to any brand:

```
1.  "{brand}" reviews
2.  "{brand}" scam OR fraud
3.  "{brand}" complaints
4.  "{brand}" legit OR trustworthy
5.  "{brand}" problems OR issues
6.  "is {brand} safe"
7.  "{brand}" reddit
8.  "{brand}" vs
```

**Notes:**
- Query 2 ("scam OR fraud") is critical for detecting red flags — never skip it.
- Query 8 ("vs") reveals which competitors the market associates with the brand.
- Always use quotes around the brand name to ensure exact-match results.

---

## Platform Queries (always run — 5 queries)

These queries check for presence on key review and discussion platforms:

```
9.   site:reddit.com "{brand}"
10.  site:trustpilot.com "{brand}"
11.  "{brand}" quora
12.  "{brand}" youtube review
13.  "{brand}" glassdoor reviews
```

**Notes:**
- `site:` queries restrict results to that specific domain.
- If the brand is B2C, Trustpilot results are especially important.
- If the brand is B2B, Glassdoor and G2 (covered in niche queries) matter more.

---

## Niche-Specific Queries

### crypto (8 queries)

```
14.  "{brand}" rug pull
15.  "{brand}" security audit OR smart contract audit
16.  "{brand}" tokenomics review
17.  "{brand}" CoinGecko OR CoinMarketCap
18.  "{brand}" DeFi risk OR DeFi scam
19.  "{brand}" hack OR exploit
20.  "{brand}" whitepaper review
21.  "{brand}" crypto regulation OR compliance
```

### igaming (7 queries)

```
14.  "{brand}" casino license OR gambling license
15.  "{brand}" payout problems OR payout speed
16.  "{brand}" rigged OR unfair
17.  "{brand}" withdrawal issues OR withdrawal delay
18.  "{brand}" AskGamblers OR Casino.org
19.  "{brand}" no deposit bonus review
20.  "{brand}" responsible gambling
```

### saas (6 queries)

```
14.  "{brand}" pricing review OR pricing comparison
15.  "{brand}" alternatives OR competitors
16.  "{brand}" G2 review OR Capterra review
17.  "{brand}" downtime OR outage OR reliability
18.  "{brand}" customer support review OR support quality
19.  "{brand}" enterprise review OR case study
```

### agency (5 queries)

```
14.  "{brand}" client reviews OR client results
15.  "{brand}" portfolio OR work examples
16.  "{brand}" clutch.co review OR clutch review
17.  "{brand}" case study results
18.  "{brand}" agency review OR agency rating
```

### ecommerce (6 queries)

```
14.  "{brand}" shipping complaints OR delivery issues
15.  "{brand}" refund policy review OR return experience
16.  "{brand}" product quality review
17.  "{brand}" BBB rating OR BBB complaints
18.  "{brand}" customer service review
19.  "{brand}" fake products OR counterfeit
```

### fintech (5 queries)

```
14.  "{brand}" security breach OR data leak
15.  "{brand}" regulation compliance OR licensed
16.  "{brand}" hidden fees OR fee structure
17.  "{brand}" FCA OR SEC OR regulated
18.  "{brand}" money safe OR funds protection
```

### healthcare (5 queries)

```
14.  "{brand}" patient reviews OR patient experience
15.  "{brand}" malpractice OR medical error
16.  "{brand}" accreditation OR certified
17.  "{brand}" HIPAA compliance OR data privacy
18.  "{brand}" doctor reviews OR provider rating
```

### legal (4 queries)

```
14.  "{brand}" client testimonials OR case results
15.  "{brand}" bar complaints OR disciplinary
16.  "{brand}" Avvo review OR Martindale rating
17.  "{brand}" settlement results OR case outcomes
```

### real_estate (4 queries)

```
14.  "{brand}" agent reviews OR broker reviews
15.  "{brand}" Zillow review OR Realtor.com
16.  "{brand}" complaints BBB OR housing complaints
17.  "{brand}" closing issues OR transaction problems
```

### travel (5 queries)

```
14.  "{brand}" TripAdvisor review
15.  "{brand}" booking problems OR reservation issues
16.  "{brand}" refund experience OR cancellation policy
17.  "{brand}" tourist scam OR travel warning
18.  "{brand}" hotel review OR service quality
```

### education (5 queries)

```
14.  "{brand}" accreditation status OR accredited
15.  "{brand}" student reviews OR student experience
16.  "{brand}" degree value OR ROI
17.  "{brand}" scam diploma OR diploma mill
18.  "{brand}" alumni reviews OR graduate outcomes
```

### general

No additional queries beyond Base + Platform (13 total).

---

## Query Execution Rules

1. **Order**: Run Base queries first (1-8), then Platform queries (9-13), then Niche-specific (14+).
2. **Total count**: 13 queries (general) to 21 queries (crypto) per brand.
3. **Comparison mode**: Run the full matrix for Brand A first, then Brand B. Do not interleave.
4. **No-data handling**: If a `WebSearch` returns zero results for a query, record `no_data` for that query and continue. Never abort the audit.
5. **Duplicate results**: The same URL may appear across multiple queries. When computing scores, de-duplicate by URL — keep only the occurrence with the highest position (lowest number = better rank).
6. **Language adaptation**: If the brand operates primarily in a non-English market (detected from the URL domain or user's language), add 3-5 queries in the local language. For example, for a Russian brand add: `"{brand}" отзывы`, `"{brand}" мошенники`, `"{brand}" жалобы`.
7. **Custom queries**: After showing the matrix, ask the user if they want to add any specific queries before starting execution. Integrate user-added queries into the Niche-specific group.
