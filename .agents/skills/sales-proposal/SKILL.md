---
name: sales-proposal
description: >-
  Client proposal generator. Creates comprehensive commercial proposals including executive summary, problem statement, solution architecture, ROI metrics, timeline, and terms, saving CLIENT-PROPOSAL.md.
---

# Skill: sales-proposal

**Role:** Generate tailored, value-driven commercial proposals and post-proposal follow-up cadences.  
**Mandatory Rules:** `customer-context.md` (mandatory), `product-context.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/{slug}/CLIENT-PROPOSAL.html` and `reports/{slug}/markdown/CLIENT-PROPOSAL.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, financial modeling, and analysis operate in English. Proposal copy and follow-ups automatically adapt to the primary language of the client.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Argument explicite fourni :** Utilise le slug du prospect (`reports/{slug}/`).
2. **Argument omis (`*`) :** Analyse l'historique récent de la conversation. Si un compte prospect fait l'objet de l'échange, déduis et réutilise son slug sans demander confirmation.
3. **Absence totale de contexte :** ARRÊT IMMÉDIAT. N'écris AUCUN fichier sur le disque. Demande une clarification :
   > *"Sur quel compte prospect souhaitez-vous exécuter cette analyse ? (ex: `proposal nom-du-prospect`)"*

> [!CAUTION]
> **Interdiction stricte :** Aucun livrable ne doit être créé directement à la racine de `reports/`.

## Trigger

Invoked via `proposal [prospect]*`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (budget sweet spot, ICP pains) and `.agents/rules/product-context.md` (packages, pricing tiers, authorized scope). Then read available workspace intelligence strictly in Markdown:
- Primary: `reports/{slug}/markdown/PROSPECT-ANALYSIS.md` ou `reports/{slug}/markdown/LEAD-QUALIFICATION.md`
- Buying Committee: `reports/{slug}/markdown/DECISION-MAKERS.md`
- Meeting Intelligence & Discovery: `reports/{slug}/markdown/MEETING-PREP.md`
- Competitive Intel & Displacement: `reports/{slug}/markdown/COMPETITIVE-INTEL.md`
- Commercial Calibration: `reports/my-company/markdown/ICP-FRAMEWORK.md`

## Workflow (3 Sequential Steps)

1. **Input Consolidation:**
   - Synthesize verified challenges, business priorities, meeting findings, and competitor gaps from existing Markdown reports.
   - Run targeted `search_web` or `read_url_content` ONLY if vital economic scope data is absent.

2. **Proposal Architecture (Mandatory Standard Order):**
   1. *Executive Summary:* 1-page C-level brief (metrics and bottom-line outcomes first).
   2. *Situation Analysis:* Confirmed operational bottlenecks with factual sources.
   3. *Recommended Solution:* Architecture and methodology strictly referencing `product-context.md`.
   4. *Scope & Milestones:* Concrete phased breakdown of deliverables and exclusions.
   5. *Delivery Timeline:* Realistic implementation schedule with built-in validation buffers.
   6. *Investment & Commercial Terms:* Pricing structure faithfully reflecting `product-context.md` (Dynamic CPM, custom SaaS per screen, or project quote — DO NOT force 3 artificial tiers if absent from product context).
   7. *Financial Business Case (ROI & Cost of Inaction):*
      - **Conservative Upside ROI:** Transparent financial model showing payback period and value multiplier.
      - **Quantified Cost of Inaction (COI):** Monthly and annual compounding cost of maintaining status quo ($\text{Identified Waste} + \text{Yield Loss} + \text{Excess Legacy Cost}$).
   8. *Delivery Team & Case Studies:* Verified proof points documented in `product-context.md`.
   9. *Immediate Next Steps:* 3 concrete actions with target decision milestones.
   Template reference: `view_file(".agents/skills/sales-proposal/references/proposal-template.md")`.

3. **Follow-up Cadence:**
   - Draft a 3-touch post-proposal re-engagement sequence (Day +2, Day +5, Day +10) with tailored value angles.

## Strict Guardrails

- ❌ Never invent pricing tiers, daily rates, or discount structures absent from `product-context.md`.
- ❌ Never commit to unlisted technical capabilities, custom integrations, or unverified SLAs.
- ✅ ROI projections must remain conservative with explicit, documented underlying assumptions.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/CLIENT-PROPOSAL.html` using `view_file(".agents/rules/references/proposal-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/CLIENT-PROPOSAL.md` using `view_file(".agents/skills/sales-proposal/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
