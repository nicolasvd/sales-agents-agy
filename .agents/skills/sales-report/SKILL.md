---
name: sales-report
description: >-
  Sales pipeline reporting agent. Aggregates all prospect audits, qualifications, and research files in the workspace into a consolidated executive pipeline report in SALES-REPORT.md.
---

# Skill: sales-report

**Role:** Aggregate workspace intelligence into an executive pipeline report and dynamically generate/update the global visual portal (`reports/index.html`).  
**Mandatory Rules:** `scoring.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/pipeline/PIPELINE-SUMMARY.html`, `reports/pipeline/markdown/PIPELINE-SUMMARY.md`, and master portal `reports/index.html`.

> [!IMPORTANT]
> **Language Governance:** Internal aggregation, mathematical rollups, and logs operate in English. Deliverable executive summaries and notes adapt to the user's primary operating language.

## Trigger

Invoked via `report` (standalone, without arguments). Aggregates all prospect directories and audit files generated across the entire workspace.

## Workflow (3 Sequential Steps)

1. **Workspace Audit Discovery & Inventory:**
   - Recursively inspect the `reports/` directory to discover all prospect subdirectories (`reports/{slug}/`) and root reports (`IDEAL-CUSTOMER-PROFILE.*`, `OBJECTION-PLAYBOOK.*`).
   - For each prospect directory, inspect available deliverables:
     `PROSPECT-ANALYSIS.*`, `LEAD-QUALIFICATION.*`, `COMPANY-RESEARCH.*`, `DECISION-MAKERS.*`, `OUTREACH-SEQUENCE.*`, `MEETING-PREP.*`, `CLIENT-PROPOSAL.*`, `COMPETITIVE-INTEL.*`.

2. **Metric Extraction & Pipeline Rollup:**
   - Extract key data per audited company:
     - Composite Prospect Score, BANT Total (/100), MEDDIC Completeness (%), Assigned Grade (A/B/C/D).
     - Top identified trigger events and primary buying committee contacts.
     - Sequence readiness score and recommended immediate next step.
   - Calculate aggregate metrics: Total audited accounts, average qualification score, grade distribution breakdown, and priority deal ranking.

3. **Dual Reporting & Master Portal Maintenance:**
   - **Executive Pipeline Deliverable:** Generate `reports/pipeline/PIPELINE-SUMMARY.html` and `reports/pipeline/markdown/PIPELINE-SUMMARY.md` using `view_file(".agents/skills/sales-report/references/output-template.md")`.
   - **Central Portal Hub (`reports/index.html`):** Read `view_file(".agents/rules/references/index-template.html")` and inject company cards for each discovered account into `{{COMPANIES_CARDS_HTML}}`. Each card features:
     - Company Name, Slug, and Grade Badge (A/B/C/D).
     - Direct links to every generated HTML deliverable.
     - Direct link to the raw machine data folder (`reports/{slug}/markdown/`).
     - Client-side search and filtering compatibility (`filterCards()`).

## Strict Guardrails

- Never invent or estimate metrics, scores, or company names absent from source audit files.
- If no prospect audits exist in `reports/`, generate a clean `PIPELINE-SUMMARY` flagging an empty pipeline.
- Every report is an immutable snapshot timestamped with generation date and UTC time.

## Mandatory Dual Output

Save all deliverables simultaneously within `reports/`:
1. **Web HTML (Humans):** `reports/pipeline/PIPELINE-SUMMARY.html` and portal hub `reports/index.html`.
2. **Raw Markdown (AI Memory):** `reports/pipeline/markdown/PIPELINE-SUMMARY.md`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory 3-link completion block:

```markdown
---
### 📁 Generated Deliverables
- 🌐 **Web / Print Version (Humans):** [PIPELINE-SUMMARY.html](reports/pipeline/PIPELINE-SUMMARY.html)
- 📄 **Raw Machine Data (AI):** [PIPELINE-SUMMARY.md](reports/pipeline/markdown/PIPELINE-SUMMARY.md)
- 📑 **Global Reports Portal:** [index.html](reports/index.html)
```
