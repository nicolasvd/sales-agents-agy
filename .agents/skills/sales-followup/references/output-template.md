# Template — FOLLOWUP-SEQUENCE.md

## Output Format

Write the complete follow-up sequence to `reports/{slug}/markdown/FOLLOWUP-SEQUENCE.md` with the following structure:

```markdown
---
slug: "[slug]"
company: "[Company]"
url: "[url or Not publicly available]"
type: "followup"
audit_date: "YYYY-MM-DD"
prospect_name: "[Prospect Name]"
scenario: "[Selected Scenario Name]"
temperature: "[Hot/Warm/Cool/Cold]"
deal_stage: "[Early/Active/Near Decision/Stalled]"
---

# Follow-Up Sequence: [Prospect Name] — [Company]

Generated: [Date]
Scenario: [Selected Scenario Name]
Prospect Temperature: [Hot/Warm/Cool/Cold]
Deal Stage: [Early/Active/Near Decision/Stalled]

---

## Prospect Context

| Field | Details |
|-------|---------|
| Prospect | [Name] |
| Company | [Company] |
| Role | [Title] |
| Last Interaction | [Type] on [Date] |
| Key Discussion Points | [Bullet list] |
| Stated Pain Points | [Bullet list] |
| Agreed Next Steps | [What was agreed] |
| Temperature | [Hot/Warm/Cool/Cold] |
| Deal Stage | [Stage] |

---

## Selected Scenario: [Scenario Name]

### Email 1: [Email Title]
**Send**: [Timing relative to last interaction]
**Channel**: Email
**Subject**: [Subject line]

[Full email body]

**Companion LinkedIn Action**: [Action + timing]
**Companion Phone Script** (if applicable): [Script]

---

### Email 2: [Email Title]
[Same format as above]

---

[Continue for all emails in sequence]

---

## Phone Scripts

### Voicemail Script 1 — [Timing]
[Full 30-second script]

### Voicemail Script 2 — [Timing]
[Full 30-second script]

---

## SMS Templates (Warm/Hot Leads Only)

1. [SMS template 1]
2. [SMS template 2]
3. [SMS template 3]

---

## Cadence Calendar

| Day | Channel | Action | Content |
|-----|---------|--------|---------|
| Day 0 | Email | Email 1 | [Brief description] |
| Day 1 | LinkedIn | Profile view | [Action] |
| Day 3 | Email | Email 2 | [Brief description] |
| ... | ... | ... | ... |

---

## Best Practices Applied

- [List of principles followed in this sequence]
- [Specific personalization choices made and why]
- [Notes on tone, timing, and channel strategy]
```

---

## Rules and Constraints

1. **Every email must add NEW value.** Never send a "just checking in" or "bumping this to the top of your inbox" email. If there is nothing new to say, do not send.
2. **Reference specific conversation points.** Generic follow-ups get deleted. Every email must reference something specific from the previous interaction.
3. **One clear next step per email.** Never give multiple CTAs. One email = one ask.
4. **Under 100 words per email.** Busy people do not read long follow-ups. Respect their time.
5. **Appropriate urgency.** Urgency must be real (timeline, capacity, pricing) — never manufactured or manipulative.
6. **Personalization is mandatory.** Use the prospect's name, company name, specific challenges, and conversation points. No [PLACEHOLDER] brackets in the final output.
7. **Professional but human tone.** Write like a helpful human, not a sales bot. Contractions are fine. Overly formal language is not.
8. **No manipulation tactics.** No fake scarcity, no guilt trips, no "I noticed you opened my email" tracking callouts.
9. **Respect the prospect's time and intelligence.** They know you want to sell. Be direct about your intent while providing genuine value.
10. **If previous analysis files exist**, incorporate their data. Do not ask the user to repeat information that is already available in `reports/{slug}/markdown/` (`PROSPECT-ANALYSIS.md`, `COMPANY-RESEARCH.md`, `MEETING-PREP.md`, or `CLIENT-PROPOSAL.md`).
