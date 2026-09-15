---
name: sales-outreach
description: >-
  Cold outreach email and LinkedIn sequence generator. Designs highly personalized 5-touch omnichannel outreach sequences based on company triggers and pains, saving OUTREACH-SEQUENCE.md.
---

# Skill: sales-outreach

**Role:** Generate highly personalized 5-touch omnichannel outreach sequences (Email + LinkedIn) strictly grounded in verified public trigger events.  
**Mandatory Rules:** `product-context.md` (mandatory), `fact-checking.md`, `output-formatting.md`, `scoring.md`.  
**Deliverables:** `reports/{slug}/OUTREACH-SEQUENCE.html` and `reports/{slug}/markdown/OUTREACH-SEQUENCE.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, trigger extraction, and scoring operate in English. Message copy automatically adapts to the primary language of the audited prospect.

## Trigger

Invoked via `outreach <prospect_name>`. Inspect available workspace intelligence first:
- `reports/{slug}/PROSPECT-ANALYSIS.html` or `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- `reports/{slug}/DECISION-MAKERS.html` or `reports/{slug}/markdown/DECISION-MAKERS.md`
- `reports/IDEAL-CUSTOMER-PROFILE.html` or `reports/markdown/IDEAL-CUSTOMER-PROFILE.md`

## Workflow (6 Sequential Steps)

1. **Context Retrieval:** Extract confirmed pains, buyer persona, and firmographics from workspace files.
2. **Trigger Event Search:** Query `search_web` for recent verifiable events (< 90 days: funding, hiring surges, product releases, tech updates). Taxonomy: `view_file(".agents/skills/sales-outreach/references/outreach-frameworks.md")`.
3. **Framework Selection:** Select the optimal pattern (Observation→Connection→Ask, Problem→Proof→Ask, Trigger Event, Mutual Connection) matching prospect maturity.
4. **5-Touch Sequence Drafting:**
   - Day 1: Email (Trigger hook + Pain bridge + Soft CTA)
   - Day 3: LinkedIn (Engage-first profile connection note)
   - Day 7: Email (Value proposition grounded in `product-context.md`)
   - Day 14: Email (Case study or relevant insight)
   - Day 21: Email (Graceful break-up touch)
5. **LinkedIn Strategy:** Craft tailored connection request and engagement prompts (< 300 characters).
6. **Outreach Readiness Scoring:** Score sequence readiness (0–100) per `scoring.md` criteria.

## Strict Guardrails

- ❌ Never draft an outreach sequence without at least one verified trigger event.
- ❌ Never mention features, capabilities, or pricing absent from `product-context.md`.
- ❌ Absolute passivity: all outputs are drafts for human review. Never send messages externally.
- ✅ Keep all cold emails strictly under 100 words with a single open-ended question CTA.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/OUTREACH-SEQUENCE.html` using `view_file(".agents/rules/references/outreach-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/OUTREACH-SEQUENCE.md` using `view_file(".agents/skills/sales-outreach/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory Browser First completion block per `output-formatting.md`:

```text
=== LIVRABLES GÉNÉRÉS ===
📄 Fichier Web : reports/{slug}/OUTREACH-SEQUENCE.html
🤖 Données IA  : reports/{slug}/markdown/OUTREACH-SEQUENCE.md

🚀 Ouvrir dans le navigateur :
open reports/{slug}/OUTREACH-SEQUENCE.html
```
