---
name: sales-contacts
description: >-
  Decision maker and buying committee identification. Maps economic buyers, champions, influencers, gatekeepers, finds public contact info and personalization anchors, saving DECISION-MAKERS.md.
---

# Skill: sales-contacts

**Role:** Identify and map the target account's buying committee, key decision-makers, and public personalization anchors.  
**Mandatory Rules:** `customer-context.md` (mandatory), `fact-checking.md` (mandatory), `scoring.md`, `output-formatting.md`.  
**Deliverables:** `reports/{slug}/DECISION-MAKERS.html` and `reports/{slug}/markdown/DECISION-MAKERS.md`.

> [!IMPORTANT]
> **Language Governance:** Internal search queries, reasoning, and role classifications operate in English. Deliverable content automatically adapts to the primary language of the prospect.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Explicit argument provided:** Extract the domain and prospect slug (`reports/{slug}/`).
2. **Omitted argument (`*`):** Analyze recent conversation history. If a prospect account is already active in the exchange, deduce and reuse its slug without prompting for confirmation.
3. **Complete absence of context:** STOP IMMEDIATELY. Write NO files to disk. Prompt the user clearly for clarification:
   > *"Which prospect account or URL would you like to analyze? (e.g., `contacts https://example.com`)"*

> [!CAUTION]
> **Strict Prohibition:** Never create any deliverable directly at the root of `reports/`.

## Trigger

Invoked via `contacts <url>`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` to identify target Buying Committee personas (Economic Buyer, Champion, Technical Evaluator). If available, inspect also:
- `reports/{slug}/markdown/COMPANY-RESEARCH.md` (or `.html` version)
- `reports/my-company/markdown/ICP-FRAMEWORK.md` (or `.html` version)

## Workflow (4 Sequential Steps)

> [!IMPORTANT]
> **Re-run & Refresh Policy:** When explicitly invoked with a target prospect URL or topic, systematically execute a fresh web exploration. Overwrite existing local reports with updated findings and today's date (`audit_date`). Never use existing local markdown files as a substitute for an explicit user re-run.

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

Display the Executive Briefing Card (Modern Markdown) at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
