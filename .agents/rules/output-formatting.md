# Rule: Output Formatting & Dual Output Standard (HTML Humans + MD AI)

> [!IMPORTANT]
> **Linguistic Hierarchy:** 1. UI Shell 100% English (headers, labels, accordions). 2. Analysis copy adapts to user prompt language (French/English). 3. Internal reasoning, logs, and schemas strictly English.

## Executive Summary (Start of Chat Response)

Every skill response begins with a concise executive summary before any deep narrative:

### 📊 Executive Summary — [Company / Subject]
- **Verdict / Score:** [Primary score/grade, e.g., 78/100 (Tier 1)]
- **Key Signals:** [Strongest signals with source in parentheses]
- **Points of Vigilance:** [Primary risk, blocker, or landmine]
- **Recommended Action:** [Single concrete next step]

## Storage Architecture: HTML for Humans & Markdown for AI

For each analysis, two distinct deliverables are created under `reports/`:
- **Visual Version (For Humans):** `reports/{slug}/{DELIVERABLE}.html` (clean SaaS UI, SVG gauges, print styling).
- **Raw Data Version (For AI):** `reports/{slug}/markdown/{DELIVERABLE}.md` (machine context). AI skills MUST ingest Markdown files exclusively — NEVER ingest `.html` files when `.md` is available.
- **Central Cockpit (`reports/index.html`):** System views live in header buttons; audited prospect accounts populate `companyGrid`.

### Folder Segregation: System Views vs. Prospect Cards
- **System Reserved Folders:** `reports/my-company/`, `reports/radar/`, and `reports/pipeline/`. Linked exclusively in header buttons. NEVER add cards for them in `companyGrid`.
- **Prospect Folders:** `reports/{slug}/` (where `{slug}` is an audited target account). Only audited prospects generate cards in `companyGrid`. When no prospects exist, `companyGrid` displays the empty state.

| Skill | Deliverable Base (.html & markdown/.md) | Scope | Reference Template |
|---|---|---|---|
| `sales-prospect` | `reports/{slug}/PROSPECT-ANALYSIS` | Prospect | `report-template.html` |
| `sales-outreach` | `reports/{slug}/OUTREACH-SEQUENCE` | Prospect | `outreach-template.html` |
| `sales-followup` | `reports/{slug}/FOLLOWUP-SEQUENCE` | Prospect | `outreach-template.html` |
| `sales-prep` | `reports/{slug}/MEETING-PREP` | Prospect | `meeting-prep-template.html` |
| `sales-proposal` | `reports/{slug}/CLIENT-PROPOSAL` | Prospect | `proposal-template.html` |
| `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION` | Prospect | `report-template.html` |
| `sales-research` | `reports/{slug}/COMPANY-RESEARCH` | Prospect | `report-template.html` |
| `sales-contacts` | `reports/{slug}/DECISION-MAKERS` | Prospect | `report-template.html` |
| `sales-competitors` | `reports/{slug}/COMPETITIVE-INTEL` | Prospect | `report-template.html` |
| `sales-objections` | `reports/{slug}/OBJECTION-PLAYBOOK` | Prospect | `battle-card-template.html` |
| `sales-icp` | `reports/my-company/ICP-FRAMEWORK` | System | `context-template.html` |
| `sales-setup` | `reports/my-company/company-dna` | System | `context-template.html` |
| `sales-radar` | `reports/radar/RADAR-DISCOVERY` | System | `radar-template.html` |
| `sales-report` | `reports/pipeline/PIPELINE-SUMMARY` | System | `pipeline-summary-template.html` |

## Mandatory Machine Metadata Standard (YAML Frontmatter)

Every Markdown deliverable written to `reports/{slug}/markdown/{DELIVERABLE}.md` MUST begin with a standardized YAML frontmatter header containing verified machine metadata:

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

Every report (except root `reports/index.html`) MUST include the cockpit return button in its `<header>`:

```html
<nav class="nav-actions">
  <a href="../index.html" class="btn-back">← Back to Portal</a>
</nav>
```
*(All deliverables reside in 1-level subdirectories like `reports/{slug}/` and use `href="../index.html"`. Styling is handled natively by the reference templates).*

## Deliverables Generated (Completion Standard)

Every skill response MUST conclude with a clean, sober block listing the created file paths and confirming that `reports/index.html` has been updated:

### 📦 Deliverables Generated
- **Web:** `reports/{slug}/{DELIVERABLE}.html`
- **AI Data:** `reports/{slug}/markdown/{DELIVERABLE}.md`
- **Portal Updated:** `reports/index.html`
