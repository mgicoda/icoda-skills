# SERM Guard — Recommendations Catalog

All recommendations for the Sentiment & Reputation Guard audit. Only include a recommendation
when its trigger condition is met based on the audit findings. Never include recommendations
that don't apply to the analyzed brand.

---

## Selection & Sorting Logic

1. Check each recommendation's **Trigger** against audit data. Only include if the condition is true.
2. Sort by priority: HIGH → MEDIUM → LOW.
3. Within the same priority, prefer lower effort (Easy before Hard).
4. Maximum **10 recommendations** in the report.
5. Always try to include at least 1 recommendation from each timeframe group if available.
6. After the generic recommendations, check the **Niche-Specific Addenda** at the bottom for
   additional recommendations specific to the detected industry.

---

## Quick Wins (1–2 weeks)

### R01 — Claim Unclaimed Review Platform Profiles

- **Trigger:** A major review platform (Trustpilot, G2, Capterra, Glassdoor, or niche equivalent) shows results for the brand but the brand has no claimed/verified profile there.
- **Priority:** HIGH
- **Effort:** Easy | **Timeframe:** 1–3 days
- **Description:** Unclaimed review profiles mean the brand has no ability to respond to reviews, update business information, or influence how it's presented on that platform. Claiming the profile is free and gives immediate control over the brand's presence.
- **Expected effect:** Enables review response capability, improves Platform Presence Score (+20 pts potential), signals active brand management to both users and LLMs.

### R02 — Respond to Negative Reviews Professionally

- **Trigger:** Negative reviews found on any review platform (Trustpilot, G2, Google, Reddit, etc.) without visible brand responses.
- **Priority:** HIGH
- **Effort:** Easy | **Timeframe:** 1–5 days
- **Description:** Unresponded negative reviews are the single most damaging reputation signal. Both human users and AI systems interpret silence as admission. A professional, empathetic response to each negative review — acknowledging the issue, offering a solution, and inviting offline resolution — transforms a negative signal into a demonstration of customer care.
- **Expected effect:** Shifts sentiment classification from Negative to Mixed or Neutral for responded reviews. Improves Search Sentiment Score and LLM Sentiment Score.

### R03 — Optimize or Create Google Business Profile

- **Trigger:** No Google Business Profile / Google Maps listing detected in search results for the brand.
- **Priority:** HIGH
- **Effort:** Easy | **Timeframe:** 1–2 days (verification may take 1–2 weeks)
- **Description:** Google Business Profile is a cornerstone of local and brand search presence. It appears prominently in search results and provides a controlled space for business info, reviews, and updates. Missing it means ceding that prime SERP real estate to competitors or uncontrolled content.
- **Expected effect:** Improves SERP Control (+owned result in brand queries), Platform Presence Score (+20 pts), and provides a direct channel for collecting and managing reviews.

### R04 — Establish Branded Reddit Presence

- **Trigger:** Reddit discussions about the brand exist but the brand has no official account engaging in them.
- **Priority:** MEDIUM
- **Effort:** Easy | **Timeframe:** 1–2 weeks (ongoing)
- **Description:** Reddit threads rank highly in search results and are increasingly used as training data for LLMs. A branded Reddit account that participates constructively — answering questions, providing updates, addressing concerns — creates positive signals both for search and AI systems. Do NOT astroturf or shill. Be transparent about being a brand representative.
- **Expected effect:** Adds positive owned/earned signals to Reddit-related queries. Improves LLM perception (Reddit content heavily influences AI training).

### R05 — Publish FAQ Page Addressing Trust Queries

- **Trigger:** Queries like "{brand} scam", "{brand} legit", "is {brand} safe" return results where the brand's own content is not in the top 5.
- **Priority:** HIGH
- **Effort:** Easy | **Timeframe:** 3–5 days
- **Description:** When people search "[brand] scam" or "[brand] legit", they should find the brand's own answer. Create a dedicated FAQ or trust page that directly addresses common concerns: legitimacy, safety, complaints process, licensing, security measures. Use FAQ schema markup. This page should rank for these queries, displacing negative or irrelevant results.
- **Expected effect:** Directly improves SERP Control for trust-related queries. Provides structured E-E-A-T signals. The FAQ schema makes this content highly citable by LLMs.

### R06 — Add Structured Data (Organization Schema)

- **Trigger:** Brand website lacks JSON-LD structured data (no Organization, WebSite, or relevant schema detected in search result snippets).
- **Priority:** MEDIUM
- **Effort:** Easy | **Timeframe:** 2–4 hours
- **Description:** Organization schema establishes the brand's entity identity for search engines and AI systems. It helps LLMs know who the brand is, what it does, and how to correctly attribute information. Without it, AI systems must guess — and they often guess wrong.
- **Expected effect:** Improves LLM Sentiment Score (content quality component, +5 pts). Helps search engines generate richer brand SERP features.

### R07 — Create llms.txt File

- **Trigger:** No llms.txt file detected for the brand's website.
- **Priority:** LOW
- **Effort:** Easy | **Timeframe:** 1 hour
- **Description:** llms.txt is an emerging standard (llmstxt.org) that lets websites provide structured context specifically for AI crawlers. It describes what the brand does, lists key pages, and provides instructions for AI systems. Early adoption signals technical sophistication and may improve AI indexing.
- **Expected effect:** Improves LLM Sentiment (content quality signal, +5 pts). Helps AI crawlers understand the brand's most important content.

### R08 — Publish Official Response to Top Negative Mentions

- **Trigger:** Specific negative articles, threads, or reviews appear in the top 5 results for any brand query.
- **Priority:** HIGH
- **Effort:** Medium | **Timeframe:** 1–2 weeks
- **Description:** For each high-visibility negative mention, create a professional response — either directly on the platform (if possible), or as a blog post/press release that can rank alongside the negative content. Address the specific claims factually. Do not attack the source. Provide evidence of resolution.
- **Expected effect:** Can shift sentiment of the surrounding SERP from Negative to Mixed. Creates counter-narratives that LLMs can reference.

### R09 — Set Up Brand Monitoring

- **Trigger:** Any negative signals detected in the audit — proactive monitoring prevents future reputation damage.
- **Priority:** MEDIUM
- **Effort:** Easy | **Timeframe:** 1 day setup
- **Description:** Set up Google Alerts, Mention.com, Brand24, or equivalent for the brand name + key negative terms ("scam", "complaint", "fraud"). This enables rapid response to new negative content before it gains traction in search and AI training data.
- **Expected effect:** Prevents future reputation damage through early detection. Does not directly affect current scores but protects against score degradation.

### R10 — Optimize Social Media Profiles for Brand Queries

- **Trigger:** Brand's social media profiles (LinkedIn, Twitter/X, Facebook) are not appearing in the top 10 results for the brand name query.
- **Priority:** MEDIUM
- **Effort:** Easy | **Timeframe:** 2–4 hours
- **Description:** Social media profiles are "owned" SERP real estate. Ensure all profiles use the exact brand name, have complete descriptions, link to the website, and are actively maintained. A filled-out LinkedIn Company page with the brand name as the page title should appear in brand search results.
- **Expected effect:** Increases SERP Control (more owned results). Each social profile in the top 10 is one less slot available for hostile content.

---

## Medium-Term (1–3 months)

### R11 — Launch Review Acquisition Campaign

- **Trigger:** Fewer than 50 total reviews across all platforms, OR low review platform presence.
- **Priority:** HIGH
- **Effort:** Medium | **Timeframe:** Ongoing (results visible in 1–2 months)
- **Description:** Proactively ask satisfied customers/clients to leave reviews on key platforms (Google, Trustpilot, G2, or niche equivalents). Use post-purchase/post-service emails, in-app prompts, or direct requests. Focus on platforms where the brand currently has the weakest presence. Never incentivize reviews in ways that violate platform policies.
- **Expected effect:** Increases Platform Presence Score. Shifts Search Sentiment toward Positive as new positive reviews appear. Creates fresh positive signals for LLM training.

### R12 — Publish Thought Leadership Content

- **Trigger:** Low E-E-A-T indicators — brand doesn't produce educational or expertise content visible in search.
- **Priority:** MEDIUM
- **Effort:** Medium | **Timeframe:** 1–3 months (ongoing)
- **Description:** Create and publish substantive content that demonstrates expertise in the brand's industry: how-to guides, industry analysis, data-driven reports, expert interviews. This content serves double duty — it ranks in search for related queries AND provides E-E-A-T signals that make LLMs more likely to trust and recommend the brand.
- **Expected effect:** Improves LLM Sentiment Score (E-E-A-T expertise +10, content quality +10). Creates additional owned search results.

### R13 — Build Media & PR Mentions

- **Trigger:** Low trust signals — few or no mentions in major publications or authoritative industry sites.
- **Priority:** MEDIUM
- **Effort:** Hard | **Timeframe:** 2–3 months
- **Description:** Execute a PR strategy to get the brand mentioned in authoritative publications. Options include: press releases for newsworthy events, guest contributions to industry outlets, expert commentary pitches, partnerships with established brands. Each authoritative mention is a strong trust signal for both search engines and LLMs.
- **Expected effect:** Improves LLM Sentiment Score (trust signals, up to +15 for press mentions). Improves authority signal for Search Sentiment weighting.

### R14 — Create Comparison Landing Pages

- **Trigger:** Competitor brands are outranking the brand for "{brand} vs {competitor}" queries.
- **Priority:** MEDIUM
- **Effort:** Medium | **Timeframe:** 2–4 weeks
- **Description:** Create "[Brand] vs [Competitor]" comparison pages on the brand's own website. Present an honest, detailed comparison that highlights the brand's strengths. These pages target the "vs" queries where users are actively deciding between options — an incredibly high-intent moment.
- **Expected effect:** Improves SERP Control for comparison queries. Creates owned content for a query pattern the brand was previously absent from.

### R15 — Start YouTube Presence

- **Trigger:** No YouTube results found for the brand across all queries.
- **Priority:** MEDIUM
- **Effort:** Medium | **Timeframe:** 1–3 months
- **Description:** Create a brand YouTube channel with content relevant to the brand's audience: product demos, tutorials, behind-the-scenes, client testimonials, industry insights. YouTube videos rank in Google search and YouTube is the second-largest search engine. YouTube content is also heavily used in AI training.
- **Expected effect:** Improves Platform Presence Score (+20 pts for YouTube). Creates additional owned video results in SERP. Provides rich media signals for LLMs.

### R16 — Quora & Reddit Content Strategy

- **Trigger:** Low presence on Quora or Reddit — few or no brand-related answers/discussions found.
- **Priority:** LOW
- **Effort:** Medium | **Timeframe:** Ongoing
- **Description:** Identify relevant questions on Quora and discussions on Reddit where the brand's expertise applies. Provide genuinely helpful answers that naturally reference the brand. Do NOT spam or post promotional content. Focus on being the most helpful answer in the thread.
- **Expected effect:** Improves Platform Presence Score (Quora +10, Reddit +20). UGC platform content heavily influences LLM training data.

### R17 — SEO for Brand-Name Queries

- **Trigger:** Brand's own website does not occupy position 1 for the exact brand name query.
- **Priority:** HIGH
- **Effort:** Medium | **Timeframe:** 1–2 months
- **Description:** If the brand doesn't rank #1 for its own name, this is a critical SEO failure. Optimize the homepage title tag, meta description, and H1 for the brand name. Build internal links to the homepage. Ensure social profiles link back. Address any duplicate content or cannibalization issues.
- **Expected effect:** Directly improves SERP Control Score (position 1 bonus +10 pts). Fundamental to all other reputation management efforts.

### R18 — Create Case Studies & Success Stories

- **Trigger:** Low E-E-A-T "experience proof" — no case studies, testimonials, or success stories found in search results.
- **Priority:** MEDIUM
- **Effort:** Medium | **Timeframe:** 2–4 weeks per case study
- **Description:** Publish detailed case studies with real metrics and outcomes. These serve as the strongest "experience" signal in E-E-A-T — they prove the brand delivers results. Include client quotes (with permission), before/after data, and specific methodologies.
- **Expected effect:** Improves LLM Sentiment Score (E-E-A-T experience proof, +10 pts). Creates rankable content for "{brand} results" and "{brand} case study" queries.

---

## Strategic (3–6 months)

### R20 — Wikipedia Page (for established brands)

- **Trigger:** No Wikipedia page exists for a brand with established notability (multiple press mentions, years of operation, significant market presence).
- **Priority:** HIGH
- **Effort:** Hard | **Timeframe:** 3–6 months
- **Description:** Wikipedia is the single highest-authority signal for LLMs. Brands with Wikipedia pages receive significantly more favorable AI treatment. However, Wikipedia has strict notability guidelines — the brand must have independent, reliable secondary sources covering it. Do not create a Wikipedia page without meeting these criteria, as it will be deleted.
- **Expected effect:** Improves LLM Sentiment Score (+10 pts for Wikipedia presence). Provides a high-authority result that typically ranks in the top 3 for brand queries.

### R21 — Comprehensive SERP Domination Strategy

- **Trigger:** SERP Control Rate below 50%.
- **Priority:** HIGH
- **Effort:** Hard | **Timeframe:** 3–6+ months
- **Description:** Execute a multi-channel strategy to occupy as many top-10 positions as possible for the brand name query. Tactics include: homepage SEO, social profile optimization, review platform presence, knowledge panel optimization, brand blog/news section, YouTube channel, Crunchbase/LinkedIn company page. The goal is to leave no room for hostile content in the top 10.
- **Expected effect:** SERP Control Rate increase of 20-40% over 6 months. Fundamentally reshapes the brand's search presence.

### R22 — Digital PR for LLM Training Data Influence

- **Trigger:** LLM Sentiment Score below 60 — brand needs to improve how AI systems perceive it.
- **Priority:** MEDIUM
- **Effort:** Hard | **Timeframe:** 3–6 months
- **Description:** LLMs are trained on web data — the more positive, authoritative content exists about the brand, the more favorably AI will present it in the future. Focus on getting coverage in sources known to be in LLM training data: Wikipedia, major news outlets, high-quality blogs, Stack Overflow / industry-specific Q&A sites, academic papers or industry reports.
- **Expected effect:** Gradually shifts LLM perception as new training data is incorporated. The highest-ROI long-term investment in AI reputation.

### R23 — Negative Content Suppression via Positive Content Creation

- **Trigger:** Negative results in the top 5 positions for brand queries.
- **Priority:** HIGH
- **Effort:** Hard | **Timeframe:** 3–6 months
- **Description:** Create and promote high-quality positive content designed to outrank existing negative results. This is NOT about removing content (which is rarely possible) — it's about pushing it down with better content. Create dedicated pages, earn media mentions, publish guest posts, and build links to positive content that targets the same keywords the negative content ranks for.
- **Expected effect:** Pushes negative results from the first page to subsequent pages, where they receive 90% less visibility. Directly improves Search Sentiment and SERP Control scores.

### R24 — Community Building Program

- **Trigger:** No positive user-generated content (UGC) found — no brand advocates or community engagement visible.
- **Priority:** MEDIUM
- **Effort:** Hard | **Timeframe:** 3–6 months
- **Description:** Build an owned community (Discord, Slack, forum, ambassador program) that generates positive UGC. Engaged community members create reviews, social posts, Reddit comments, and content that creates a web of positive brand signals. This is especially important for crypto and iGaming brands where community trust is paramount.
- **Expected effect:** Creates a sustainable source of positive UGC across platforms. Improves Platform Presence and Search Sentiment over time.

### R25 — Authority Building Through Industry Partnerships

- **Trigger:** Low authority signals — brand is not associated with established industry players.
- **Priority:** LOW
- **Effort:** Hard | **Timeframe:** 3–6 months
- **Description:** Partner with established brands, industry associations, or thought leaders. Co-publish reports, speak at conferences, join industry groups. These partnerships create association signals that boost both search authority and LLM trust assessment.
- **Expected effect:** Improves LLM Sentiment Score (authoritative mentions, +10 pts). Creates earned positive SERP results from partner sites.

### R26 — Ongoing Reputation Monitoring & Rapid Response System

- **Trigger:** Any negative signals detected — a brand needs a systematic approach to reputation management.
- **Priority:** MEDIUM
- **Effort:** Medium | **Timeframe:** 1 week setup, then ongoing
- **Description:** Implement a systematic reputation monitoring and response workflow: (1) automated monitoring of brand mentions, (2) severity classification protocol, (3) response templates for common scenarios, (4) escalation procedures for crises, (5) quarterly reputation audit re-runs using this skill.
- **Expected effect:** Prevents reputation deterioration. Catches new negative content early. Maintains and gradually improves scores over time.

---

## Niche-Specific Addenda

These recommendations apply IN ADDITION to the universal ones above, based on the detected niche.

### Crypto

- **RC01 — Display Security Audit Badges:** If the project has undergone a smart contract audit (Certik, Trail of Bits, OpenZeppelin), display the badge prominently and create a dedicated security page. (Trigger: crypto brand with no visible audit mentions. Priority: HIGH)
- **RC02 — Optimize CoinGecko/CoinMarketCap Profile:** Ensure complete, verified profiles on both platforms with accurate data, links, and descriptions. (Trigger: crypto token/protocol with incomplete listings. Priority: HIGH)
- **RC03 — Publish Transparent Tokenomics Page:** Create a detailed, easily understandable tokenomics page with vesting schedules, allocation breakdowns, and governance info. (Trigger: "tokenomics" queries return non-brand results. Priority: MEDIUM)

### iGaming

- **RG01 — Create Licensing Authority Page:** Publish a dedicated page listing all gambling licenses, jurisdictions, and regulatory compliance status with verifiable license numbers. (Trigger: igaming brand without visible licensing info. Priority: HIGH)
- **RG02 — Publish Payout Proof/Statistics:** Create a transparency page showing payout percentages, RTP for games, and withdrawal processing times. (Trigger: "payout" queries associated with complaints. Priority: HIGH)
- **RG03 — Optimize AskGamblers/Casino Guru Profile:** Claim and optimize profiles on major casino review aggregators. (Trigger: igaming brand missing from key review sites. Priority: MEDIUM)

### SaaS

- **RS01 — Optimize G2/Capterra Profiles:** Claim profiles, respond to reviews, add product screenshots, pricing info, and feature comparisons. (Trigger: SaaS brand with unclaimed or incomplete review profiles. Priority: HIGH)
- **RS02 — Publish Integration Partner Directory:** Create a page listing all integrations — this content ranks well for "{brand} integrations" and signals ecosystem maturity. (Trigger: SaaS brand without visible integrations page. Priority: MEDIUM)
- **RS03 — Create "{brand} vs" Comparison Hub:** Build a comparison center covering top 5 competitors. (Trigger: "alternatives" query dominated by competitor content. Priority: MEDIUM)

### Agency

- **RA01 — Optimize Clutch.co Profile:** Complete all sections, request client reviews, showcase top projects. (Trigger: agency without Clutch profile or with incomplete profile. Priority: HIGH)
- **RA02 — Publish Detailed Case Studies with Metrics:** Real numbers, real results, real client names. (Trigger: agency with no visible case studies. Priority: HIGH)
- **RA03 — Create Industry-Specific Service Pages:** Dedicated pages for each vertical the agency serves. (Trigger: agency website too generic, doesn't rank for niche queries. Priority: MEDIUM)
