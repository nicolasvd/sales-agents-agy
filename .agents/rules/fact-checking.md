# Rule: Fact-Checking & Web Intelligence

> [!IMPORTANT]
> **Language Directive:** Internal reasoning, search queries, validation labels, and logs operate strictly in English. Citation labels and factual extracts in customer-facing reports adapt to the prospect's language (e.g., French: Confirmé / Estimé / Non disponible publiquement; English: Confirmed / Estimated / Not publicly available).

## Source Hierarchy (Descending Reliability)

1. Official company web pages (direct web extraction — always prioritize first)
2. Official business registries: BCE/CBE Belgium, SIRENE France, Companies House UK
3. Specialized business press: TechCrunch, Forbes, Les Échos, Trends-Tendances, PUB.be
4. SaaS & customer feedback databases: Crunchbase, G2, Capterra, Glassdoor (via `search_web`)
5. LinkedIn: via `search_web` only (no direct personal profile scraping)

## Browsing Protocol & Chrome Fallback Strategy

### Priority 1: Fast Extraction (`read_url_content`)
- Default method across all target URLs (ultra-low latency execution).
- Validated if extracted content is structured, intelligible, and contains **> 200 characters of meaningful text**.

### Priority 2 (Fallback): Chrome Subagent (`/browser`)
Mandatorily delegate URL access to the Chrome subagent (`/browser`) in the following cases:
1. **Dynamic Client-Side Rendering Required:** Single Page Applications (SPA: React, Vue, Next.js, Angular) without pre-rendered server HTML.
2. **Bot Protections & Blocking:** Pages guarded by Cloudflare, anti-scraping mechanisms, JavaScript challenges, or returning HTTP 403/429 errors.
3. **Insufficient Useful Content:** When `read_url_content` returns **< 200 characters of useful text** (e.g., "Please enable JavaScript" or empty loading state).
- **Goal:** Extract the fully hydrated post-execution DOM to capture true ground truth.

## Systematic Pages to Explore

For each target prospect, probe in this specific sequence (gracefully ignore 404s):
1. `/` — Homepage (mandatory)
2. `/about` or `/about-us` — Leadership team, mission, founders
3. `/pricing` or `/plans` — Budget indicators, tiers, and market segment
4. `/careers` or `/jobs` — Growth velocity, open technical/business needs
5. `/blog` — Marketing maturity, recent announcements, discussed challenges
6. `/integrations` or `/partners` — Software ecosystem and technical stack
7. `/customers` or `/case-studies` — Social proof, testimonials, and client typologies

## 5 Systematic `search_web` Queries

Execute for every prospect (replace `[NAME]` with verified company name):
1. `"[NAME]" funding OR raised OR revenue OR valuation`
2. `"[NAME]" employees OR headcount OR hiring site:linkedin.com`
3. `"[NAME]" news OR announcement` (filter within past 12 months)
4. `"[NAME]" review OR reviews site:g2.com OR site:capterra.com`
5. `"[NAME]" alternative OR competitor OR "vs "`

## Mandatory Citation Standards

Every single factual metric or claim MUST include its provenance:
- **Confirmed / Confirmé:** Explicit statement in a verified primary source  
  → `€3.4M Revenue (Source: Forbes Belgium, June 2026)`
- **Estimated / Estimé:** Triangulated from secondary signals  
  → `~40 employees (Estimated from LinkedIn + open job postings, Sept 2026)`
- **Not publicly available / Non disponible publiquement:** When information is absent — never invent.

## Data Freshness Windows

| Data Type | Validity Window |
|---|---|
| Scoring Data (Budget, Need) | ≤ 18 months |
| Trigger Events (Funding, M&A, Executive Hires) | ≤ 90 days |
| Historical Data (Contextual Background Only) | > 18 months → explicitly tag as "Historical" |
