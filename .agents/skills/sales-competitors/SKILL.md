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
1. **Argument explicite fourni :** Extrais le domaine et le slug du prospect (`reports/{slug}/`).
2. **Argument omis (`*`) :** Analyse l'historique récent de la conversation. Si un compte prospect fait l'objet de l'échange, déduis et réutilise son slug sans demander confirmation.
3. **Absence totale de contexte :** ARRÊT IMMÉDIAT. N'écris AUCUN fichier sur le disque. Demande une clarification :
   > *"Sur quel compte prospect souhaitez-vous exécuter cette analyse ? (ex: `competitors https://exemple.com`)"*

> [!CAUTION]
> **Interdiction stricte :** Aucun livrable ne doit être créé directement à la racine de `reports/`.

## Trigger

Invoked via `competitors <url>`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (ICP core pains and tech stack sweet spot) and `.agents/rules/product-context.md` (authorized positioning). If available, inspect also:
- `reports/{slug}/markdown/COMPANY-RESEARCH.md` ou `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- `reports/my-company/markdown/ICP-FRAMEWORK.md` (technographic profile & baseline tools)

## Workflow (5 Sequential Steps)

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

Display the Terminal Summary Block at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
