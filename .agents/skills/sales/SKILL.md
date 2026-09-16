---
name: sales
description: >-
  Main orchestrator for the AI Sales Team. Coordinates all 15 specialized sales workflows including workspace onboarding, prospect discovery & radar, lead qualification, contacts mapping, outreach sequences, and pipeline reporting.
---

# AI Sales Team — Main Orchestrator

100% declarative B2B sales intelligence platform for Google Antigravity.
Orchestrates 15 autonomous sales skills and 5 internal subagents without scripts or external runtime dependencies.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, coordination, logs, and scratchpad schemas operate strictly in English. Customer-facing deliverables (HTML and Markdown) automatically adapt to the primary language of the audited company.

## Command Index

| Command | Skill | Dual Output (Web HTML + AI Markdown) |
|---|---|---|
| `setup [url]` | `sales-setup` | `reports/my-company/company-dna.html` (+ `.agents/rules/product-context.md`, `.agents/rules/customer-context.md`) |
| `qualify <url>` | `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION.html` (+ `markdown/`) |
| `research <url>` | `sales-research` | `reports/{slug}/COMPANY-RESEARCH.html` (+ `markdown/`) |
| `contacts <url>` | `sales-contacts` | `reports/{slug}/DECISION-MAKERS.html` (+ `markdown/`) |
| `prospect <url>` | `sales-prospect` | `reports/{slug}/PROSPECT-ANALYSIS.html` (+ `markdown/`) |
| `outreach <prospect>` | `sales-outreach` | `reports/{slug}/OUTREACH-SEQUENCE.html` (+ `markdown/`) |
| `followup <prospect>` | `sales-followup` | `reports/{slug}/FOLLOWUP-SEQUENCE.html` (+ `markdown/`) |
| `prep <url>` | `sales-prep` | `reports/{slug}/MEETING-PREP.html` (+ `markdown/`) |
| `proposal <client>` | `sales-proposal` | `reports/{slug}/CLIENT-PROPOSAL.html` (+ `markdown/`) |
| `competitors <url>` | `sales-competitors` | `reports/{slug}/COMPETITIVE-INTEL.html` (+ `markdown/`) |
| `icp <description>` | `sales-icp` | `reports/IDEAL-CUSTOMER-PROFILE.html` (+ `markdown/`) |
| `objections <topic>` | `sales-objections` | `reports/OBJECTION-PLAYBOOK.html` (+ `markdown/`) |
| `radar [topic/event]` | `sales-radar` | `reports/pipeline/RADAR-DISCOVERY.html` (+ `markdown/`) |
| `report` | `sales-report` | `reports/PIPELINE-SUMMARY.html` (Index Hub) |
| `update [framework]` | `framework-update` | Workspace sync via GitHub REST API (Sanctuary-safe) |

## Dispatching Logic

When a command is invoked, load the corresponding skill instruction file from `.agents/skills/<skill>/SKILL.md`.

### System & Maintenance Dispatching
Commands requesting framework or workspace updates (`update`, `update framework`) are routed to `.agents/skills/framework-update/SKILL.md` to ensure strict isolation from commercial workflows.

### Full 360° Prospect Audit (`prospect <url>`)
Orchestrated by `sales-prospect` via disk scratchpad (`.agents/.scratchpad/prospect_{slug}.json`) across two sequential waves:
- **Wave 1 (Independent Research):** `sales-sub-company`, `sales-sub-contacts`, `sales-sub-competitive`
- **Wave 2 (Synthesis & Strategy):** `sales-sub-opportunity` (BANT/MEDDIC scoring), `sales-sub-strategy` (Outreach plan)

### Mandatory Transverse Rules
Every execution must strictly load and enforce:
- `AGENTS.md` (root entrypoint, absolute passivity, zero hallucination)
- `.agents/rules/fact-checking.md` (primary source verification, strict citations, demo profile check)
- `.agents/rules/scoring.md` (deterministic BANT, MEDDIC, Urgency scorecards)
- `.agents/rules/product-context.md` (product offering, fixed pricing, scope exclusions)
- `.agents/rules/customer-context.md` (ICP definition, target personas, qualification thresholds)
- `.agents/rules/output-formatting.md` (terminal summary block, Dual Output, 3-link completion block)
