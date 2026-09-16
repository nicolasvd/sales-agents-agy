# Rule: Output Formatting & Dual Output Standard (HTML Humans + MD AI)

> [!IMPORTANT]
> **Linguistic Precedence (Strict Hierarchy):**
> 1. **HTML Shell & UI Structure:** Always 100% in English (headers, navigation, labels, table headers, gauges, metric names, accordions).
> 2. **Generated Analysis & Copy:** Strictly adapts to the language of the user prompt (e.g., French prompt = content drafted in French inside the English UI shell; English prompt = 100% English).
> 3. **Internal Reasoning & Logs:** Scratchpad schemas, internal deliberation, subagent delegation, and tool arguments operate strictly in English.

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
| `sales-report` | `reports/pipeline/PIPELINE-SUMMARY.html` | `reports/pipeline/markdown/PIPELINE-SUMMARY.md` | `index-template.html` |
| `sales-radar` | `reports/pipeline/RADAR-DISCOVERY.html` | `reports/pipeline/markdown/RADAR-DISCOVERY.md` | `radar-template.html` |

## Completion Block Standard (Browser First)

Every skill response MUST conclude with this standardized closing block. Execute the command `open reports/{slug}/{REPORT_NAME}.html` via the shell if context allows, or display the block below:

```text
=== LIVRABLES GÉNÉRÉS ===
📄 Fichier Web : reports/{slug}/{REPORT_NAME}.html
🤖 Données IA  : reports/{slug}/markdown/{REPORT_NAME}.md

🚀 Ouvrir dans le navigateur :
open reports/{slug}/{REPORT_NAME}.html
```

