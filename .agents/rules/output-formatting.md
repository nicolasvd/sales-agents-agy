# Rule: Output Formatting & Modern Markdown Chat Standard

> [!IMPORTANT]
> **Linguistic Hierarchy:** UI Shell 100% English. Analysis copy adapts to user prompt language (French/English). Internal reasoning strictly English.

## Executive Briefing Card (Modern Chat Response Standard)

Every skill response begins with a modern Executive Briefing Card in rich GitHub Markdown. Never use legacy CLI monospace banners (`=== COMPLETE ===`) or ASCII progress bars (`████░░`):

### 🎯 [Skill Name] : [Company Name / Subject]

> [!TIP]
> **Verdict:** **[Grade / Classification]** (Score: [XX]/100) | **Core Opportunity:** [1-sentence strategic synthesis]

| Dimension / KPI | Score / Value | Weight & Contribution | Verified Key Signal |
|---|---|---|---|
| **[Dimension 1]** | **[Score]** | [Weight]% → **[Contribution] pts** | [Key factual evidence with source] |
| **[Dimension 2]** | **[Score]** | [Weight]% → **[Contribution] pts** | [Key factual evidence with source] |

- **💡 Strategic Angle:** [Hook connecting trigger to solution pillar]
- **⚠️ Point of Vigilance:** [Primary risk, blocker, or landmine]
- **⚡ Next Action:** `[skill] [url]` targeting [Role / Contact].

## Typography & HTML Sanitation Standard (Zero-LaTeX)

- ❌ **Zero LaTeX in Deliverables:** NEVER use LaTeX syntax (`$\rightarrow$`, `\times`, `$$...$$`, `\approx`, `\le`, `\ge`, `\$`) in HTML or Markdown deliverables.
- **Universal Characters & Entities:**
  - Arrows: Use `→` in Markdown or `&rarr;` / `→` in HTML (never `$\rightarrow$` or `->`).
  - Multiplication: Use `×` in Markdown or `&times;` / `×` in HTML (never `\times` or `*`).
  - Inequalities: Use `≤` / `&le;` and `≥` / `&ge;`. Currency: Raw `$` or `€` (never `\$`).

## Storage Architecture: HTML for Humans & Markdown for AI

For each analysis, two deliverables are generated under `reports/`:
- **Visual Version (Humans):** `reports/{slug}/{DELIVERABLE}.html` (clean SaaS UI, SVG gauges, print styling).
- **Raw Data Version (AI):** `reports/{slug}/markdown/{DELIVERABLE}.md` (AI skills ingest Markdown exclusively).
- **Central Cockpit (`reports/index.html`):** System views live in header buttons; audited prospects populate `companyGrid`.

### Folder Segregation: System Views vs. Prospect Cards
- **System Reserved:** `reports/my-company/`, `reports/radar/`, `reports/pipeline/` (linked in header buttons only, never in `companyGrid`).
- **Prospect Folders:** `reports/{slug}/` (only audited target accounts generate cards in `companyGrid`).

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

## Machine Metadata Standard (YAML Frontmatter)

Every Markdown deliverable begins with standard frontmatter:

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
competitive_context: { incumbent_tools: ["{Tool1}"], switching_cost: "Low|Med|High" }
top_triggers: ["{Verified Trigger (< 90 days)}"]
---
```

## Navigation Standard & Deliverables Generated

Every report includes the return button in `<header>`:
```html
<nav class="nav-actions"><a href="../index.html" class="btn-back">← Back to Portal</a></nav>
```

Every skill concludes with the completion block:

### 📦 Deliverables Generated
- **Web (Interactive):** `reports/{slug}/{DELIVERABLE}.html`
- **AI Data (Markdown):** `reports/{slug}/markdown/{DELIVERABLE}.md`
- **Portal Updated:** `reports/index.html`
