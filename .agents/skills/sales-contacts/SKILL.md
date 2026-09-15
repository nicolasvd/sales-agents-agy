---
name: sales-contacts
description: >-
  Decision maker and buying committee identification. Maps economic buyers, champions, influencers, gatekeepers, finds public contact info and personalization anchors, saving DECISION-MAKERS.md.
---

# Skill: sales-contacts

**Role:** Identify and map the target account's buying committee, key decision-makers, and public personalization anchors.  
**Mandatory Rules:** `fact-checking.md` (mandatory), `scoring.md`, `output-formatting.md`.  
**Deliverables:** `reports/{slug}/DECISION-MAKERS.html` and `reports/{slug}/markdown/DECISION-MAKERS.md`.

> [!IMPORTANT]
> **Language Governance:** Internal search queries, reasoning, and role classifications operate in English. Deliverable content automatically adapts to the primary language of the prospect.

## Trigger

Invoked via `contacts <url>`. If available, inspect:
- `reports/{slug}/COMPANY-RESEARCH.html` or `reports/{slug}/markdown/COMPANY-RESEARCH.md`
- `reports/IDEAL-CUSTOMER-PROFILE.html` or `reports/markdown/IDEAL-CUSTOMER-PROFILE.md`

## Workflow (4 Sequential Steps)

1. **Targeted Leadership Identification:**
   - Execute `read_url_content` across company leadership pages: `/team`, `/about`, `/leadership`, `/board`.
   - Query `search_web` for executive profiles: `"[Company Name]" CEO OR CTO OR VP site:linkedin.com` and related leadership titles.
   - Standard search protocol: `view_file(".agents/skills/sales-contacts/references/contact-protocol.md")`.

2. **Buying Committee Functional Mapping:**
   - Classify discovered stakeholders into 4 committee roles:
     - **Economic Buyer:** Executive with ultimate budget approval authority (CEO, CFO, VP).
     - **Champion:** Day-to-day user or operational leader who directly feels the pain and advocates for the solution.
     - **Influencer:** Technical evaluator or operational peer providing input (IT, Legal, Security).
     - **Gatekeeper:** Executive assistant, procurement coordinator, or operational screener.

3. **Personalization Anchor Extraction:**
   - For primary targets, identify verified public anchors:
     - Recent LinkedIn posts, articles, or comments (< 90 days)
     - Podcast appearances, interviews, or conference talks
     - Stated professional priorities and public initiatives

4. **Contact Access Scoring (0–25 pts):**
   - Apply the Authority scorecard from `scoring.md` to compute the deterministic Contact Access score.

## Strict Guardrails

- Missing email addresses must be recorded as `Not publicly available` — never guess, extrapolate, or hallucinate.
- Domain email patterns must be strictly labeled as `[Estimated]` when inferred from organizational naming conventions.
- Never attempt direct scraping of authenticated LinkedIn profiles — use public search snippets via `search_web`.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/DECISION-MAKERS.html` using `view_file(".agents/rules/references/report-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/DECISION-MAKERS.md` using `view_file(".agents/skills/sales-contacts/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory 3-link completion block:

```markdown
---
### 📁 Generated Deliverables
- 🌐 **Web / Print Version (Humans):** [DECISION-MAKERS.html](reports/{slug}/DECISION-MAKERS.html)
- 📄 **Raw Machine Data (AI):** [DECISION-MAKERS.md](reports/{slug}/markdown/DECISION-MAKERS.md)
- 📑 **Global Reports Portal:** [index.html](reports/index.html)
```
