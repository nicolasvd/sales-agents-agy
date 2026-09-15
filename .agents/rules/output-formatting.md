# Rule: Output Formatting & Dual Output Standard (HTML Humans + MD AI)

> [!IMPORTANT]
> **Language Directive:** Internal reasoning, subagent delegation, logs, and scratchpad schema operate strictly in English. Deliverable content automatically adapts to the primary language of the audited company.

## Terminal Summary Block (Mandatory at Start of Chat Response)

This block appears FIRST in the conversational response before any in-depth narrative:

```text
=== [SKILL NAME IN UPPERCASE] : [COMPANY NAME] ===

[PRIMARY SCORE] : [X]/100  Grade : [A/B/C/D]
[Sub-scores if applicable, e.g.: Budget: 18/25  Authority: 20/25]

Top Signals:
  1. [Strongest signal — factual source in parentheses]
  2. [Signal 2 — source]
  3. [Signal 3 — source]

Red Flags:
  1. [Primary point of vigilance]
  2. [Secondary point of vigilance if applicable]

Recommended Action: [Concrete action statement, single concise line]
```

## Storage Architecture: HTML for Humans & Markdown for AI

For each prospect analysis, two distinct deliverables are created under `reports/`:
- **Visual Version (For Humans):** Written directly to `reports/{slug}/{DELIVERABLE}.html`. Polished typography, interactive cards, inline SVG score gauges, and `@media print` optimized A4 styles.
- **Raw Data Version (For AI):** Stored in `reports/{slug}/markdown/{DELIVERABLE}.md` to serve as clean machine context for future agent sessions.
- **Central Dashboard:** `reports/index.html` aggregates and links all generated HTML deliverables.

| Skill | Web Version (Humans) | Raw Version (AI) | Reference Template |
|---|---|---|---|
| `sales-prospect` | `reports/{slug}/PROSPECT-ANALYSIS.html` | `reports/{slug}/markdown/PROSPECT-ANALYSIS.md` | `report-template.html` |
| `sales-outreach` | `reports/{slug}/OUTREACH-SEQUENCE.html` | `reports/{slug}/markdown/OUTREACH-SEQUENCE.md` | `outreach-template.html` |
| `sales-prep` | `reports/{slug}/MEETING-PREP.html` | `reports/{slug}/markdown/MEETING-PREP.md` | `meeting-prep-template.html` |
| `sales-proposal` | `reports/{slug}/CLIENT-PROPOSAL.html` | `reports/{slug}/markdown/CLIENT-PROPOSAL.md` | `proposal-template.html` |
| `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION.html` | `reports/{slug}/markdown/LEAD-QUALIFICATION.md` | `report-template.html` |
| `sales-research` | `reports/{slug}/COMPANY-RESEARCH.html` | `reports/{slug}/markdown/COMPANY-RESEARCH.md` | `report-template.html` |
| `sales-contacts` | `reports/{slug}/DECISION-MAKERS.html` | `reports/{slug}/markdown/DECISION-MAKERS.md` | `report-template.html` |
| `sales-competitors` | `reports/{slug}/COMPETITIVE-INTEL.html` | `reports/{slug}/markdown/COMPETITIVE-INTEL.md` | `report-template.html` |
| `sales-report` | `reports/PIPELINE-SUMMARY.html` | `reports/markdown/PIPELINE-SUMMARY.md` | `index-template.html` |

## Mandatory Completion Block Standard (Workspace-Relative Links)

Every skill response MUST conclude with this exact summary block using strictly workspace-relative links for universal portability:

```markdown
---
### 📁 Generated Deliverables
- 🌐 **Web / Print Version (Humans):** [FILE-NAME.html](reports/{slug}/FILE-NAME.html)
- 📄 **Raw Machine Data (AI):** [FILE-NAME.md](reports/{slug}/markdown/FILE-NAME.md)
- 📑 **Global Reports Portal:** [index.html](reports/index.html)
```
