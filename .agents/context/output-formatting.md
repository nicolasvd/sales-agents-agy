# Rule: Output Formatting & Modern Markdown Chat Standard

> [!IMPORTANT]
> **Linguistic Hierarchy & Chat Mirroring:**
> - **Internal Engine (100% Technical English):** All `SKILL.md` instructions, declarative rules, HTML templates, scratchpads, and execution logs operate strictly in technical English.
> - **Conversational Chat (Strict Language Mirroring):** Conversational chat responses systematically mirror the user's prompt language (French for French, English for English), regardless of the audited prospect's country or language.
> - **Report Deliverables (`reports/`):** Universal English UI shell and frontmatter schema. Analytical deliverable copy adapts to the target market's business language.

## Conversational Chat Standard (Direct Markdown)

Deliver executive insights directly in natural, clean Markdown (bold headings, bullet points, inline bold for metrics, inline code for commands). Do not wrap conversational text in text code blocks or monospace delimiters.
- **Tone & Structure:** Start with a concise executive summary (verdict/grade, key signals with cited sources, points of vigilance, and actionable next steps).
- **Flexibility:** Adapt the presentation structure to the specific sales domain (e.g., MEDDIC breakdown, A-R-C objection handling, or chronological outreach sequence).

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

## Universal Cockpit Navigation & Deliverables Generated

Every report generated within the workspace links back to `reports/index.html` via the standard navigation button defined in the reference templates.

Every skill concludes its response with the standardized completion block:

### 📦 Deliverables Generated
- **Web (Interactive):** `reports/{slug}/{DELIVERABLE}.html`
- **AI Data (Markdown):** `reports/{slug}/markdown/{DELIVERABLE}.md`
- **Portal Updated:** `reports/index.html`
