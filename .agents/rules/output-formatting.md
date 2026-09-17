# Rule: Output Formatting & Dual Output Standard (HTML Humans + MD AI)

> [!IMPORTANT]
> **Linguistic Precedence (Strict Hierarchy):**
> 1. **HTML Shell & UI Structure:** Always 100% in English (headers, navigation, labels, table headers, gauges, metric names, accordions).
> 2. **Generated Analysis & Copy:** Strictly adapts to the language of the user prompt (e.g., French prompt = content drafted in French inside the English UI shell; English prompt = 100% English).
> 3. **Internal Reasoning & Logs:** Scratchpad schemas, internal deliberation, subagent delegation, and tool arguments operate strictly in English.

## Executive Summary (Start of Chat Response)

Every skill response begins directly with a concise executive summary in natural Markdown before any in-depth narrative:

### 📊 Executive Summary — [Company / Subject]
- **Verdict / Score:** [Primary score, rating or qualification grade, e.g., 78/100 (Tier 1)]
- **Key Signals:**
  - [Strongest signal — source in parentheses]
  - [Secondary signal — source]
- **Points of Vigilance:**
  - [Primary risk, blocker, or landmine]
- **Recommended Action:** [Single concrete, actionable next step]

## Storage Architecture: HTML for Humans & Markdown for AI

For each analysis, two distinct deliverables are created under `reports/`:
- **Visual Version (For Humans):** Written to `reports/{path}/{DELIVERABLE}.html`. Polished typography, interactive cards, inline SVG score gauges, and `@media print` styles.
- **Raw Data Version (For AI):** Stored in `reports/{path}/markdown/{DELIVERABLE}.md` to serve as clean machine context for future agent sessions. Downstream AI skills MUST ingest Markdown files exclusively — NEVER ingest `.html` files when `.md` is available.
- **Central Dashboard:** `reports/index.html` aggregates and links all generated HTML deliverables.

| Skill | Deliverable Base (.html & markdown/.md) | Reference Template |
|---|---|---|
| `sales-prospect` | `reports/{slug}/PROSPECT-ANALYSIS` | `report-template.html` |
| `sales-outreach` | `reports/{slug}/OUTREACH-SEQUENCE` | `outreach-template.html` |
| `sales-followup` | `reports/{slug}/FOLLOWUP-SEQUENCE` | `outreach-template.html` |
| `sales-prep` | `reports/{slug}/MEETING-PREP` | `meeting-prep-template.html` |
| `sales-proposal` | `reports/{slug}/CLIENT-PROPOSAL` | `proposal-template.html` |
| `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION` | `report-template.html` |
| `sales-research` | `reports/{slug}/COMPANY-RESEARCH` | `report-template.html` |
| `sales-contacts` | `reports/{slug}/DECISION-MAKERS` | `report-template.html` |
| `sales-competitors` | `reports/{slug}/COMPETITIVE-INTEL` | `report-template.html` |
| `sales-objections` | `reports/{slug}/OBJECTION-PLAYBOOK` | `battle-card-template.html` |
| `sales-icp` | `reports/my-company/ICP-FRAMEWORK` | `context-template.html` |
| `sales-report` | `reports/pipeline/PIPELINE-SUMMARY` | `pipeline-summary-template.html` |
| `sales-radar` | `reports/radar/RADAR-DISCOVERY` | `radar-template.html` |
| `sales-setup` | `reports/my-company/company-dna` | `context-template.html` |

## Mandatory Machine Metadata Standard (YAML Frontmatter)

Every Markdown deliverable written to `reports/{path}/markdown/{DELIVERABLE}.md` MUST begin with a standardized YAML frontmatter header containing verified machine metadata:

```yaml
---
slug: "{slug}"
company_name: "{company_name}"
domain: "{domain}"
audit_date: "YYYY-MM-DD"
scoring:
  prospect_score: {0-100}
  lead_grade: "A|B|C|D"
  bant_total: {0-100}
  meddic_completeness_pct: {0-100}
primary_contacts:
  economic_buyer: "{Name or Not publicly available}"
  champion: "{Name or Not publicly available}"
competitive_context:
  incumbent_tools: ["{Tool1}", "{Tool2}"]
  switching_cost: "Low|Medium|High"
top_triggers:
  - "{Verified Trigger 1 (< 90 days)}"
---
```

## Universal Hub & Spoke Navigation Standard (HTML Deliverables)

No HTML deliverable is a dead end. Every report generated within the workspace (except the root portal `reports/index.html`) MUST include the standard cockpit return button in its `<header>`:

```html
<nav class="nav-actions">
  <a href="../index.html" class="btn-back">← Back to Portal</a>
</nav>
```
*(All deliverables reside in subdirectories like `reports/{slug}/`, `reports/my-company/`, `reports/radar/`, or `reports/pipeline/` and use `href="../index.html"`. Styling is handled natively by the reference templates).*

## Deliverables Generated (Completion Standard)

Every skill response MUST conclude with a clean, sober block listing the created file paths and confirming that `reports/index.html` has been updated:

### 📦 Deliverables Generated
- **Web :** `reports/{path}/{DELIVERABLE}.html`
- **Données IA :** `reports/{path}/markdown/{DELIVERABLE}.md`
- **Portail mis à jour :** `reports/index.html`
