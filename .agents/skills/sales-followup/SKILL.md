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

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Argument explicite fourni :** Utilise le slug du prospect (`reports/{slug}/`).
2. **Argument omis (`*`) :** Analyse l'historique récent de la conversation. Si un compte prospect fait l'objet de l'échange, déduis et réutilise son slug sans demander confirmation.
3. **Absence totale de contexte :** ARRÊT IMMÉDIAT. N'écris AUCUN fichier sur le disque. Demande une clarification :
   > *"Sur quel compte prospect souhaitez-vous exécuter cette analyse ? (ex: `followup nom-du-prospect`)"*

> [!CAUTION]
> **Interdiction stricte :** Aucun livrable ne doit être créé directement à la racine de `reports/`.

## Trigger

Invoked via `followup [prospect]*`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (persona priorities, target deal velocity) and `.agents/rules/product-context.md`. Then inspect available workspace context strictly in Markdown:
- Initial Sequence & Touches: `reports/{slug}/markdown/OUTREACH-SEQUENCE.md`
- Meeting Notes & Engagements: `reports/{slug}/markdown/MEETING-PREP.md`
- Proposal Terms & Scope: `reports/{slug}/markdown/CLIENT-PROPOSAL.md`
- Contact Coordinates: `reports/{slug}/markdown/DECISION-MAKERS.md`
- Core Prospect Diagnostic: `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`

## Workflow (4 Sequential Steps)

1. **Engagement History Audit:**
   - Review prior touchpoints: count of touches, last channel used, time elapsed, commitments from meeting prep or proposal files.
   - Detect response signals: silence, email opens/clicks, partial interest, objection raised, or stalled contract review.

2. **Tactical Scenario Selection:**
   - Select 1 of 5 standardized lifecycle scenarios aligned with `scenario-library.md`:
     - **Scenario 1 (Post-Discovery Meeting):** 3 touches (Recap + Value Reinforcement + Decision Nudge).
     - **Scenario 2 (Post-Demo):** 4 touches (Recap & Resources + Address Objections + Social Proof + Decision Timeline).
     - **Scenario 3 (Post-Proposal):** 5 touches (Delivery + Walkthrough Offer + Value-Add Insight + Direct Check-In + Breakup).
     - **Scenario 4 (Ghost Recovery / Stalled Deal):** 3 touches (Pattern Interrupt + New Value Angle + Honest Breakup).
     - **Scenario 5 (Strategic Nurture):** Low-touch ongoing monthly value drops without selling pressure.
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

Display the Terminal Summary Block at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
