---
name: sales-prep
description: >-
  Meeting preparation brief generator. Synthesizes prospect intelligence, key talking points, discovery questions, and tailored objection prep for upcoming sales calls, saving MEETING-PREP.md.
---

# Skill: sales-prep

**Role:** Synthesize comprehensive, tactical meeting preparation briefs for high-stakes sales conversations.  
**Mandatory Rules:** `product-context.md` (mandatory), `fact-checking.md`, `output-formatting.md`.  
**Deliverables:** `reports/{slug}/MEETING-PREP.html` and `reports/{slug}/markdown/MEETING-PREP.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, participant research, and analysis operate in English. Brief content automatically adapts to the primary language of the audited company.

## Trigger

Invoked via `prep <url>`. Read all available reports in the workspace:
- `reports/{slug}/PROSPECT-ANALYSIS.html` or `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- `reports/{slug}/DECISION-MAKERS.html` or `reports/{slug}/markdown/DECISION-MAKERS.md`
- `reports/{slug}/LEAD-QUALIFICATION.html` or `reports/{slug}/markdown/LEAD-QUALIFICATION.md`
- `reports/{slug}/COMPETITIVE-INTEL.html` or `reports/{slug}/markdown/COMPETITIVE-INTEL.md`

## Workflow (2 Sequential Steps)

1. **Targeted Research Gap Fill:**
   - Execute `search_web` for recent updates (< 30 days) regarding the account and key meeting participants.
   - Run `read_url_content` on newly discovered public pages or product releases.
   - Map attendee roles, tenure, and public perspectives via search.

2. **Brief Construction (10 Standardized Sections):**
   1. *Company Snapshot:* 2-minute executive overview (business model, stage, key metrics).
   2. *Participant Profiles:* Titles, seniority, background, and likely individual priorities.
   3. *Business Situation:* Verified current context, growth initiatives, and confirmed challenges.
   4. *Competitive Context:* Existing tooling, lock-in level, and switching friction.
   5. *Key Discussion Angles:* Top 3 prioritized narrative bridges to explore.
   6. *Strategic Discovery Questions:* 5 open-ended questions based on SPIN/MEDDIC.
   7. *Anticipated Objections:* Top 3 likely objections with empathetic acknowledge-and-reframe talk tracks.
   8. *Success Metrics:* Measurable criteria for prospect ROI validation.
   9. *Competitive Landmines:* Critical topics, legacy sensitivities, and traps to avoid.
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

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory 3-link completion block:

```markdown
---
### 📁 Generated Deliverables
- 🌐 **Web / Print Version (Humans):** [MEETING-PREP.html](reports/{slug}/MEETING-PREP.html)
- 📄 **Raw Machine Data (AI):** [MEETING-PREP.md](reports/{slug}/markdown/MEETING-PREP.md)
- 📑 **Global Reports Portal:** [index.html](reports/index.html)
```
