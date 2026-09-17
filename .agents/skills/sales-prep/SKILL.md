---
name: sales-prep
description: >-
  Meeting preparation brief generator. Synthesizes prospect intelligence, key talking points, discovery questions, and tailored objection prep for upcoming sales calls, saving MEETING-PREP.md.
---

# Skill: sales-prep

**Role:** Synthesize comprehensive, tactical meeting preparation briefs for high-stakes sales conversations.  
**Mandatory Rules:** `customer-context.md` (mandatory), `product-context.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/{slug}/MEETING-PREP.html` and `reports/{slug}/markdown/MEETING-PREP.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, participant research, and analysis operate in English. Brief content automatically adapts to the primary language of the audited company.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Argument explicite fourni :** Utilise le slug du prospect (`reports/{slug}/`).
2. **Argument omis (`*`) :** Analyse l'historique récent de la conversation. Si un compte prospect fait l'objet de l'échange, déduis et réutilise son slug sans demander confirmation.
3. **Absence totale de contexte :** ARRÊT IMMÉDIAT. N'écris AUCUN fichier sur le disque. Demande une clarification :
   > *"Sur quel compte prospect souhaitez-vous exécuter cette analyse ? (ex: `prep nom-du-prospect`)"*

> [!CAUTION]
> **Interdiction stricte :** Aucun livrable ne doit être créé directement à la racine de `reports/`.

## Trigger

Invoked via `prep [prospect]*`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (target persona pains and buying criteria) and `.agents/rules/product-context.md`. Then read all available reports strictly in Markdown:
- `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- `reports/{slug}/markdown/DECISION-MAKERS.md`
- `reports/{slug}/markdown/LEAD-QUALIFICATION.md`
- `reports/{slug}/markdown/COMPETITIVE-INTEL.md`

## Workflow (2 Sequential Steps)

1. **Upstream Ingestion & Targeted Gap Fill:**
   - Ingest confirmed attendees from `DECISION-MAKERS.md` and competitor gaps from `COMPETITIVE-INTEL.md`.
   - DO NOT re-research baseline company or competitor data already in Markdown files.
   - Restrict `search_web` strictly to breaking updates (< 15 days) and specific attendee background not yet captured.

2. **Brief Construction (10 Standardized Sections):**
   1. *Company Snapshot:* 2-minute executive overview (business model, stage, key metrics).
   2. *Participant Profiles:* Titles, seniority, background, and likely individual priorities from `DECISION-MAKERS.md`.
   3. *Business Situation:* Verified current context, growth initiatives, and confirmed challenges.
   4. *Competitive Context:* Existing tooling, lock-in level, and switching friction from `COMPETITIVE-INTEL.md`.
   5. *Key Discussion Angles:* Top 3 prioritized narrative bridges to explore.
   6. *Strategic Discovery Questions:* 5 open-ended SPIN/MEDDIC questions directly exposing incumbent stack gaps identified in `COMPETITIVE-INTEL.md`.
   7. *Anticipated Objections:* Top 3 likely objections with empathetic acknowledge-and-reframe talk tracks.
   8. *Success Metrics:* Measurable criteria for prospect ROI validation.
   9. *Competitive Landmines:* Critical topics, legacy sensitivities, and traps to avoid based on competitor battle cards.
   10. *Proposed Next Steps:* 2–3 concrete closing commitments with timelines.
   Template reference: `view_file(".agents/skills/sales-prep/references/meeting-brief-template.md")`.

## Strict Guardrails

- Discovery questions must be exploratory and open-ended, never premature sales pitches.
- All product and pricing references must strictly adhere to `product-context.md`.
- Keep the brief concise and actionable (≤ 2 pages equivalent for quick pre-meeting review).

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/MEETING-PREP.html` using `view_file(".agents/rules/references/meeting-prep-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/MEETING-PREP.md` using `view_file(".agents/skills/sales-prep/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
