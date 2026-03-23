# icoda Skills — Claude Skills & Agent Skills for AI Marketing

A collection of open-source **Claude skills** (agent skills) built by [icoda](https://icoda.io) for marketing, SEO, and AI optimization teams. Each skill installs in one click and runs directly in [claude.ai](https://claude.ai).

## Available Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [aeo-audit](./aeo-audit) | AEO & AI Visibility Audit — scores your site 0–100 for AI discoverability | [↓ Download .skill](./aeo-audit/aeo-audit.skill) |
| [serm-guard](./serm-guard) | SERM & Online Reputation Audit — scores brand reputation 0–100 across search, reviews, and AI perception | [↓ SKILL.md](./serm-guard/SKILL.md) |

---

## serm-guard — SERM & Online Reputation Audit

> A **Claude skill** that performs a comprehensive brand reputation audit across search engines, review platforms, forums, and social media — and generates a scored, visual HTML report in one conversation.

### What it audits

| Dimension | Weight | What's analyzed |
|-----------|--------|-----------------|
| 🔍 Search Sentiment | 35% | Sentiment of top-10 results per query, weighted by position and source authority |
| 🤖 LLM Sentiment | 30% | How AI systems (ChatGPT, Claude, Perplexity) perceive the brand — trust signals, red flags, E-E-A-T |
| 🎯 SERP Control | 20% | % of top-10 results the brand owns, earns, or loses to hostile sources |
| 📊 Platform Presence | 15% | Coverage across Trustpilot, Google Reviews, Reddit, LinkedIn, and niche platforms |

### Output

- **Overall score 0–100** with color-coded breakdown (green / yellow / orange / red)
- **Sentiment heatmap** across all search queries and positions
- **Top 10 prioritized recommendations** grouped by timeframe (Quick Wins / Medium-term / Strategic)
- **Inline HTML report** — ready to share or save as PDF
- **Comparison mode** — side-by-side analysis for 2 brands

### Usage examples

```
Run a SERM audit for stripe.com
```
```
Аудит репутации для Binance — что пишут в сети?
```
```
Is notion.so legit? Check reviews and complaints.
```
```
Compare HubSpot vs Salesforce reputation in search
```

### Trigger keywords

This skill activates for requests about:
- SERM audit, ORM check, reputation analysis, reputation score
- "is [brand] legit", "[brand] reviews", "[brand] scam check"
- brand sentiment analysis, online complaints, what do people say about [brand]
- **Russian:** аудит репутации, SERM анализ, репутация бренда, что пишут о бренде

Works in English and Russian.

---

## aeo-audit — AEO & AI Visibility Audit

> A **Claude skill** that audits any website for AI search readiness and generates a scored, print-ready HTML/PDF report in one conversation.

### What it checks

| Category | What's analyzed |
|----------|-----------------|
| 🤖 AI Bot Access | robots.txt rules for GPTBot, ClaudeBot, PerplexityBot, Google-Extended |
| 🏷️ Structured Data | Schema.org JSON-LD types, llms.txt presence and quality |
| ⚙️ Technical | HTTPS, XML sitemap, canonical tags, crawlability signals |
| 📝 Content Structure | Headings hierarchy, FAQ sections, citation-friendly formatting |

### Output

- **Score 0–100** with weighted category breakdown
- **ROI-ranked recommendations** — highest-impact fixes listed first
- **Print-ready HTML report** — open in browser, save as PDF

### How to install this Claude skill

1. Download [`aeo-audit.skill`](./aeo-audit/aeo-audit.skill)
2. Open [claude.ai](https://claude.ai) → **Settings → Skills**
3. Click **Install from file** and select `aeo-audit.skill`
4. Start a new chat — Claude will automatically recognize AEO audit requests

### Usage examples

```
Run a full AEO audit for stripe.com
```
```
Проверь сайт icoda.io на AI-видимость и сделай PDF-отчёт
```
```
Check if GPTBot and ClaudeBot are blocked in robots.txt for notion.so
```
```
Compare hubspot.com and salesforce.com — which is better optimized for AI search?
```

### Trigger keywords

This agent skill activates for requests about:
- AEO, GEO, AIO audit or analysis
- AI visibility, AI indexing, AI crawlability
- robots.txt checks for AI bots
- Schema markup / structured data for AI systems
- llms.txt presence
- Comparison of sites for AI search readiness

Works in English and Russian.

---

## Contributing

Each agent skill lives in its own directory with a `SKILL.md` at the root. PRs are welcome — especially new Claude skills for marketing and AI optimization workflows.

## License

MIT © [icoda](https://icoda.io)
