---
name: sales-report
description: >-
  Sales pipeline reporting agent. Aggregates all prospect audits, qualifications, and research files in the workspace into a consolidated executive pipeline report in SALES-REPORT.md.
---

# Skill: sales-report

**Role:** Aggregate workspace intelligence into an executive pipeline report and dynamically generate/update the global visual portal (`reports/index.html`).  
**Mandatory Rules:** `scoring.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:**
- **Primary:** `reports/pipeline/PIPELINE-SUMMARY.html` & `reports/pipeline/markdown/PIPELINE-SUMMARY.md`
- **Master Hub:** `reports/index.html` (auto-synced with `reports/my-company/company-dna.html` & `reports/radar/RADAR-DISCOVERY.html`)

> [!IMPORTANT]
> **Language Governance:** Internal aggregation, mathematical rollups, and logs operate in English. Deliverable executive summaries and notes adapt to the user's primary operating language.

## Trigger

Invoked via `report` (standalone, without arguments). Aggregates all prospect directories and audit files generated across the entire workspace.
- **Demo Profile Guardrail:** Verify context files per `fact-checking.md`. If demo marker (`Acme AI Automation Inc.` or unconfigured `customer-context.md`) is detected, prepend the canonical warning banner in chat and display a visible warning badge in `reports/index.html` and pipeline summary.

## Workflow (3 Sequential Steps)

1. **Workspace Audit Discovery & Inventory:**
   - Recursively inspect `reports/` to discover all prospect subdirectories (`reports/{slug}/`).
   - Check radar-level intelligence files (`reports/radar/RADAR-DISCOVERY.html`, `reports/radar/markdown/RADAR-DISCOVERY.md`).
   - Ingest raw data exclusively from Markdown files (`reports/{slug}/markdown/*.md`) — NEVER parse `.html` files for metric extraction.
   - For each prospect, inspect available deliverables:
     `PROSPECT-ANALYSIS.md`, `LEAD-QUALIFICATION.md`, `COMPANY-RESEARCH.md`, `DECISION-MAKERS.md`, `OUTREACH-SEQUENCE.md`, `MEETING-PREP.md`, `CLIENT-PROPOSAL.md`, `COMPETITIVE-INTEL.md`.

2. **Deterministic YAML Frontmatter Extraction & Pipeline Rollup:**
   - Parse the structured YAML frontmatter block at the top of each Markdown file directly:
     - `scoring.prospect_score`, `scoring.lead_grade`, `scoring.bant_total`, `scoring.meddic_completeness_pct`.
     - `primary_contacts.economic_buyer`, `primary_contacts.champion`.
     - `competitive_context.incumbent_tools`, `competitive_context.switching_cost`.
     - `top_triggers`.
   - Do NOT rely on fragile text heuristics or table regexes when YAML metadata is present.
   - Calculate aggregate metrics: Total audited accounts, average qualification score, grade distribution breakdown, and priority deal ranking.

3. **Pipeline Report Generation & Portal Sync:**
   - **Executive Pipeline Deliverable:** Generate `reports/pipeline/PIPELINE-SUMMARY.html` using `view_file(".agents/rules/references/pipeline-summary-template.html")` and `reports/pipeline/markdown/PIPELINE-SUMMARY.md` using `view_file(".agents/skills/sales-report/references/output-template.md")`.
   - **Master Portal Hub (`reports/index.html`):** Read `view_file(".agents/rules/references/index-template.html")` and inject company cards for each discovered account into `{{COMPANIES_CARDS_HTML}}`. Each card features:
     - Company Name, Slug, and Grade Badge (A/B/C/D).
     - Direct links to every generated HTML deliverable.
     - Direct link to the raw machine data folder (`reports/{slug}/markdown/`).
     - Client-side search and filtering compatibility (`filterCards()`).
   - **Satellite Views Sync:** Refresh `reports/my-company/company-dna.html` using `view_file(".agents/rules/references/context-template.html")`. If `reports/radar/markdown/RADAR-DISCOVERY.md` exists, recompile `reports/radar/RADAR-DISCOVERY.html` using `view_file(".agents/rules/references/radar-template.html")` and its source signals. Ensure both views remain accessible and linked from the portal header.

## Strict Guardrails

- Never invent or estimate metrics, scores, or company names absent from source audit files.
- If no prospect audits exist in `reports/`, generate a clean `PIPELINE-SUMMARY` flagging an empty pipeline.
- Every report is an immutable snapshot timestamped with generation date and UTC time.

## Mandatory Dual Output

Save all deliverables simultaneously within `reports/`:
1. **Web HTML (Humans):** `reports/pipeline/PIPELINE-SUMMARY.html` and portal hub `reports/index.html`.
2. **Raw Markdown (AI Memory):** `reports/pipeline/markdown/PIPELINE-SUMMARY.md`.

Conclude your response with the executive summary and standard completion block per `output-formatting.md`.
