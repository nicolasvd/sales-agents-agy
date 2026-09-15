---
name: sales-proposal
description: >-
  Client proposal generator. Creates comprehensive commercial proposals including executive summary, problem statement, solution architecture, ROI metrics, timeline, and terms, saving CLIENT-PROPOSAL.md.
---

# Skill: sales-proposal

**Role:** Generate tailored, value-driven commercial proposals and post-proposal follow-up cadences.  
**Mandatory Rules:** `product-context.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/{slug}/CLIENT-PROPOSAL.html` and `reports/{slug}/markdown/CLIENT-PROPOSAL.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, financial modeling, and analysis operate in English. Proposal copy and follow-ups automatically adapt to the primary language of the client.

## Trigger

Invoked via `proposal <client_name>`. Read available workspace intelligence:
- `reports/{slug}/PROSPECT-ANALYSIS.html` or `reports/{slug}/LEAD-QUALIFICATION.html`
- `reports/{slug}/DECISION-MAKERS.html` (economic buyer and evaluation committee)
- `reports/IDEAL-CUSTOMER-PROFILE.html` (commercial calibration)
- `.agents/rules/product-context.md` (packages, pricing tiers, authorized scope — mandatory)

## Workflow (3 Sequential Steps)

1. **Input Consolidation:**
   - Synthesize verified challenges, business priorities, and stakeholder goals from existing reports.
   - Run targeted `search_web` or `read_url_content` if vital economic scope data is absent.

2. **Proposal Architecture (Mandatory Standard Order):**
   1. *Executive Summary:* 1-page C-level brief (metrics and bottom-line outcomes first).
   2. *Situation Analysis:* Confirmed operational bottlenecks with factual sources.
   3. *Recommended Solution:* Architecture and methodology strictly referencing `product-context.md`.
   4. *Scope & Milestones:* Concrete phased breakdown of deliverables.
   5. *Delivery Timeline:* Realistic implementation schedule with built-in validation buffers.
   6. *Investment & Commercial Terms:* Fixed pricing strictly derived from `product-context.md`.
   7. *Conservative ROI Projection:* Transparent financial model showing payback period and value multiplier.
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

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory Browser First completion block per `output-formatting.md`:

```text
=== LIVRABLES GÉNÉRÉS ===
📄 Fichier Web : reports/{slug}/CLIENT-PROPOSAL.html
🤖 Données IA  : reports/{slug}/markdown/CLIENT-PROPOSAL.md

🚀 Ouvrir dans le navigateur :
open reports/{slug}/CLIENT-PROPOSAL.html
```
