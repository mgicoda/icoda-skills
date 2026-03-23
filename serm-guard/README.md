# serm-guard — SERM & Online Reputation Audit

> A **Claude skill** that performs a comprehensive brand reputation audit across search engines, review platforms, forums, and social media — and generates a scored, visual HTML report in one conversation.

## What it audits

| Dimension | Weight | What's analyzed |
|-----------|--------|-----------------|
| 🔍 Search Sentiment | 35% | Sentiment of top-10 results per query, weighted by position and source authority |
| 🤖 LLM Sentiment | 30% | How AI systems (ChatGPT, Claude, Perplexity) perceive the brand — trust signals, red flags, E-E-A-T |
| 🎯 SERP Control | 20% | % of top-10 results the brand owns, earns, or loses to hostile sources |
| 📊 Platform Presence | 15% | Coverage breadth across Trustpilot, Google Reviews, Reddit, LinkedIn, niche platforms |

## Output

- **Overall score 0–100** with color-coded breakdown (green / yellow / orange / red)
- **Sentiment heatmap** across all search queries and positions
- **Top 10 prioritized recommendations** grouped by timeframe (Quick Wins / Medium-term / Strategic)
- **Inline HTML report** — ready to share or save
- **Comparison mode** — side-by-side analysis for 2 brands

## Supported niches

Auto-detected from initial searches: `crypto/web3`, `iGaming/casino`, `SaaS`, `marketing agency`, `e-commerce`, `fintech`, `healthcare`, `legal`, `real estate`, `travel`, `education`, `general`

Each niche gets a tailored query matrix and niche-specific recommendations.

## How to install

1. Download [`SKILL.md`](./SKILL.md) along with the `references/` and `assets/` folders
2. Open [claude.ai](https://claude.ai) → **Settings → Skills**
3. Click **Install from file** and select the skill
4. Start a new chat — Claude will automatically recognize reputation audit requests

## Usage examples

```
Run a SERM audit for stripe.com
```
```
Is notion.so legit? Check reviews and complaints.
```
```
Compare HubSpot vs Salesforce reputation in search
```

## Trigger keywords

Activates for requests about:
- SERM audit, ORM check, reputation analysis, reputation score
- "is [brand] legit", "[brand] reviews", "[brand] scam check"
- brand sentiment analysis, online complaints, what do people say about [brand]

## File structure

```
serm-guard/
├── SKILL.md                          # Main skill definition (10-step workflow)
├── assets/
│   └── chat-report-template.html     # Inline HTML report template
└── references/
    ├── niche-queries.md              # Query matrices per industry (13–21 queries)
    ├── scoring.md                    # Scoring formulas and component weights
    └── recommendations-catalog.md   # 26 recommendations with triggers and ROI
```

## Tools used

- `WebSearch` — no external APIs required

---

MIT © [icoda](https://icoda.io)
