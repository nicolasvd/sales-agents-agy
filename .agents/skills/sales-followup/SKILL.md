---
name: sales-followup
description: >-
  Follow-up sequence generator for engaged leads, stalled deals, or no-response situations across email, LinkedIn, and phone, saving FOLLOWUP-SEQUENCE.md.
---

# Skill: sales-followup

**Role:** Generate adaptive multi-touch follow-up cadences across email, LinkedIn, and phone for stalled deals, unanswered outreach, or engaged leads.  
**Mandatory Rules:** `customer-context.md` (mandatory), `product-context.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/{slug}/FOLLOWUP-SEQUENCE.html` and `reports/{slug}/markdown/FOLLOWUP-SEQUENCE.md`.

> [!IMPORTANT]
> **Language Governance:** Internal scenario selection and follow-up strategy operate in English. Drafted messages automatically adapt to the primary language of the prospect.

## Trigger

Invoked via `followup <prospect_name>`. Mandatorily inspect `.agents/rules/customer-context.md` (persona priorities, target deal velocity) and `.agents/rules/product-context.md`. Then inspect available workspace context:
- `reports/{slug}/OUTREACH-SEQUENCE.html` or `reports/{slug}/markdown/OUTREACH-SEQUENCE.md` (initial sequence history)
- `reports/{slug}/DECISION-MAKERS.html` or `reports/{slug}/markdown/DECISION-MAKERS.md` (contact coordinates)

## Workflow (4 Sequential Steps)

1. **Engagement History Audit:**
   - Review prior touchpoints: count of touches, last channel used, time elapsed.
   - Detect response signals: silence, email opens/clicks, partial interest, or stalling.

2. **Tactical Scenario Selection:**
   - Select 1 of 4 specialized follow-up frameworks:
     - **Scenario A (No-Response Breakup):** 3 progressive touches leading to a polite, high-status breakup note.
     - **Scenario B (Stalled Deal Re-Ignition):** Value-add nurture injecting new urgency or market insights.
     - **Scenario C (Post-Objection Reframe):** Targeted follow-up addressing specific reservations raised.
     - **Scenario D (Internal Champion Multi-Threading):** Expanding lateral buy-in across technical and operational peers.
   - Script library reference: `view_file(".agents/skills/sales-followup/references/scenario-library.md")`.

3. **Incremental Value Personalization:**
   - Every single follow-up must deliver fresh value: a relevant industry article, newly released trigger event, or specific operational tip. Never send "just checking in" messages.

4. **Omnichannel Orchestration:**
   - Alternate intelligently between Email, LinkedIn message, and phone touch scripts based on available contact channels.

## Strict Guardrails

- Maximum 3 follow-up attempts without response before triggering the final breakup email.
- Every CTA must be a low-friction open discovery question — never demand a call on early follow-ups.
- ❌ Absolute passivity: all messages are drafts for human review. Never send external communications.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/FOLLOWUP-SEQUENCE.html` using `view_file(".agents/rules/references/outreach-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/FOLLOWUP-SEQUENCE.md` using `view_file(".agents/skills/sales-followup/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory Browser First completion block per `output-formatting.md`:

```text
=== LIVRABLES GÉNÉRÉS ===
📄 Fichier Web : reports/{slug}/FOLLOWUP-SEQUENCE.html
🤖 Données IA  : reports/{slug}/markdown/FOLLOWUP-SEQUENCE.md

🚀 Ouvrir dans le navigateur :
open reports/{slug}/FOLLOWUP-SEQUENCE.html
```
