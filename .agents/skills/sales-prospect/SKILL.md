---
name: sales-prospect
description: >-
  Pure 2-wave prospect 360° audit orchestrator. Coordinates 5 internal subagents via scratchpad JSON, calculates Prospect Score, and produces reports/{slug}/PROSPECT-ANALYSIS.html and .md.
---

# Skill: sales-prospect

**Role:** Pure orchestrator for the 5 internal subagents — full 360° B2B prospect audit.  
**Required Rules:** `scoring.md`, `output-formatting.md`.  
**Output:** `reports/{slug}/PROSPECT-ANALYSIS.html` & `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`.  
**Invoked Subagents:** `sales-sub-company`, `sales-sub-contacts`, `sales-sub-competitive`, `sales-sub-opportunity`, `sales-sub-strategy`.

## ⛔ Blocking Rule (Strict Tool De-Gating)

> **You have NO web navigation or external search tools.**
> It is STRICTLY FORBIDDEN to call `read_url_content` or `search_web`.
> You MUST delegate all data extraction and intelligence gathering to subagents via `start_subagent`.

### Authorized Tools for Orchestrator
- `create_file` (scratchpad initialization, final reports)
- `view_file` (reading consolidated scratchpad, ICP profile, templates)
- `edit_file` (scratchpad metadata updates)
- `start_subagent` (launching internal subagents)
- ❌ **FORBIDDEN:** `read_url_content`, `search_web`, `run_command`

## Invocation Trigger

Invoked via chat command: `prospect <url>`.  
If available, read: `reports/IDEAL-CUSTOMER-PROFILE.html` / `markdown/` via `view_file`.

## Workflow — Scratchpad State Machine

### 1. Scratchpad Initialization
1. Extract domain and normalize company name → `{slug}` (e.g., `socialsky`).
2. Initialize `.agents/.scratchpad/prospect_{slug}.json` via `create_file`:
```json
{
  "meta": {
    "url": "<url>",
    "slug": "{slug}",
    "status": "wave1_started"
  },
  "wave1": {
    "company_data": null,
    "contacts_data": null,
    "competitive_data": null
  },
  "wave2": {
    "opportunity_data": null,
    "strategy_data": null
  }
}
```

### 2. Wave 1 — Factual Intelligence Gathering (Pure Delegation)
Launch Wave 1 subagents sequentially:
```
start_subagent("sales-sub-company")     → populates wave1.company_data
start_subagent("sales-sub-contacts")    → populates wave1.contacts_data
start_subagent("sales-sub-competitive") → populates wave1.competitive_data
```
Read `.agents/.scratchpad/prospect_{slug}.json` via `view_file` and verify `meta.status == "wave1_complete"`.  
**STOPPING BARRIER:** NEVER launch Wave 2 if `meta.status != "wave1_complete"`.

### 3. Wave 2 — Synthesis & Strategy (Pure Delegation)
Launch Wave 2 subagents sequentially:
```
start_subagent("sales-sub-opportunity") → populates wave2.opportunity_data (conditioned on wave1_complete)
start_subagent("sales-sub-strategy")    → populates wave2.strategy_data
```
Verify `meta.status == "wave2_complete"`.

### 4. Final Deliverables & Reporting (Dual Output: HTML + Markdown)
1. Read `.agents/.scratchpad/prospect_{slug}.json` via `view_file`.
2. Calculate composite Prospect Score per `scoring.md`:
   `Prospect Score = (BANT * 0.50) + (MEDDIC% * 0.30) + (Urgency * 0.20)`
3. **Generate Raw Machine Markdown:** `create_file("reports/{slug}/markdown/PROSPECT-ANALYSIS.md")` following:
   `view_file(".agents/skills/sales-prospect/references/output-template.md")`.
4. **Generate Standalone Interactive HTML:** `create_file("reports/{slug}/PROSPECT-ANALYSIS.html")` instantiating:
   `view_file(".agents/rules/references/report-template.html")` (substitute placeholders with verified data and inline SVG gauges).
5. Output terminal summary block and Browser First completion block per `output-formatting.md`.

## Constraints
- Zero direct browsing: all factual data originates strictly from subagents via scratchpad.
- The `sales-sub-*` subagents are internal engine components: never expose internal task traces in executive reports.
- Deliverable content automatically adapts to the primary language of the audited company.
