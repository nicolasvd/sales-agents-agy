---
name: sales-competitors
description: >-
  Competitive intelligence and battle card generator. Identifies direct/indirect competitors, compares features, pricing, and positioning, and creates competitive battle cards in COMPETITIVE-INTEL.md.
---

# Skill: sales-competitors

**Role:** Analyze the prospect's incumbent technology stack, map competitive presence, and produce actionable battle cards.  
**Mandatory Rules:** `customer-context.md` (mandatory), `product-context.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/{slug}/COMPETITIVE-INTEL.html` and `reports/{slug}/markdown/COMPETITIVE-INTEL.md`.

> [!IMPORTANT]
> **Language Governance:** Internal technology detection, competitive gap analysis, and notes operate in English. Deliverable content automatically adapts to the primary language of the prospect.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Explicit argument provided:** Extract the domain and prospect slug (`reports/{slug}/`).
2. **Omitted argument (`*`):** Analyze recent conversation history. If a prospect account is already active in the exchange, deduce and reuse its slug without prompting for confirmation.
3. **Complete absence of context:** STOP IMMEDIATELY. Write NO files to disk. Prompt the user clearly for clarification:
   > *"Which prospect account or URL would you like to analyze? (e.g., `competitors https://example.com`)"*

> [!CAUTION]
> **Strict Prohibition:** Never create any deliverable directly at the root of `reports/`.

## Trigger

Invoked via `competitors <url>`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (ICP core pains and tech stack sweet spot) and `.agents/rules/product-context.md` (authorized positioning). If available, inspect also:
- `reports/{slug}/markdown/COMPANY-RESEARCH.md` or `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- `reports/my-company/markdown/ICP-FRAMEWORK.md` (technographic profile & baseline tools)

## Workflow (5 Sequential Steps)

> [!IMPORTANT]
> **Re-run & Refresh Policy:** When explicitly invoked with a target prospect URL or topic, systematically execute a fresh web exploration. Overwrite existing local reports with updated findings and today's date (`audit_date`). Never use existing local markdown files as a substitute for an explicit user re-run.

1. **Current Tooling Detection:**
   - Execute `read_url_content` across integration and partner directories: `/integrations`, `/partners`, `/ecosystem`.
   - Query `search_web` for stack disclosures: `"[Company Name]" site:stackshare.io`, `"[Company Name]" uses OR "built with"`.

2. **Competitive Categorization:**
   - Categorize detected tools into 4 distinct groups:
     - **Direct Competitor:** Alternative operating in our exact category.
     - **Indirect Competitor:** Alternative solving the same business friction with a different paradigm.
     - **Complementary Tool:** Software that cleanly integrates with our solution.
     - **Displaceable Legacy Tool:** Tool that our solution directly replaces or consolidates.

3. **Battle Card Formulation:**
   - Build a tactical battle card for each identified direct competitor (maximum 4 rivals):
     - Our key strengths vs. Their key strengths
     - Our prioritized attack angles vs. Their likely counter-attacks
     - Objection reframing scripts and differentiation talk tracks
   - Reference template: `view_file(".agents/skills/sales-competitors/references/battle-card-template.md")`.

4. **Capability Gap Analysis:**
   - Map functional shortcomings in the prospect's incumbent stack that our offering addresses, verified via public user reviews (G2, Capterra) or job posting requirements.

5. **Switching Cost Evaluation:**
   - Determine switching friction (Low / Medium / High) based on integration depth, historical tenure, and operational lock-in.

## Strict Guardrails

- ❌ Never disparage a competitor without cited, public factual proof.
- ❌ Zero unverified product claims: capabilities and differentiators must strictly originate from `product-context.md`.
- Every identified product gap must reference a verifiable public review or job spec in parentheses.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/COMPETITIVE-INTEL.html` using `view_file(".agents/rules/references/report-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/COMPETITIVE-INTEL.md` using `view_file(".agents/skills/sales-competitors/references/output-template.md")`.

Display the Executive Briefing Card (Modern Markdown) at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
