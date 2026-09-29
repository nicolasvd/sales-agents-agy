---
name: sales-prospect
description: Pure 2-wave prospect 360° audit orchestrator. Coordinates Wave 1 research agents, Wave 2 analyst, and independent reviewer QA gate via Markdown scratchpad, generating dual output reports.
---

# Skill: sales-prospect

**Role:** End-to-end orchestrator for the 360° B2B prospect audit pipeline.  
**Architecture:** Antigravity 2.0 multi-agent pipeline with deterministic QA gate and circuit breaker.  
**Required Context:** `.agents/context/product-context.md`, `.agents/context/customer-context.md`, `.agents/context/scoring.md`, `.agents/context/output-formatting.md`.  
**Required Rules:** `.agents/rules/fact-checking.md`.  
**Final Outputs:**  
- Web HTML (Humans): `reports/{slug}/PROSPECT-ANALYSIS.html`  
- Raw Markdown (AI Memory): `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`  

---

## ⛔ Operational Invariants & Tool Usage

- **Zero Direct Browsing:** The orchestrator never searches the web or fetches web pages directly. All data collection is performed by subagents.
- **Pure Markdown Scratchpad:** All intermediate data exchanges operate strictly in Markdown format within `.agents/.scratchpad/{slug}/`. No serialization files are permitted.
- **Authorized Orchestrator Tools:** `invoke_subagent`, `manage_subagents`, `send_message`, `view_file`, `write_to_file`, `replace_file_content`.

---

## Execution Protocol

### Step 0 — Target Resolution & Pre-Flight Context Gate

1. **Target Account Resolution:**
   - Resolve target domain or URL from user prompt.
   - If omitted, inherit active prospect slug from conversation context.
   - If missing entirely, stop and prompt user:
     > *"Which prospect account or URL would you like to analyze? (e.g., `prospect https://example.com`)"*
   - Normalize target domain to `{slug}` (e.g., `acme-corp`).

2. **Pre-Flight Context Verification:**
   - Read `.agents/context/product-context.md` via `view_file`.
   - If the file contains unconfigured template placeholders (`[Insert`) or lacks defined product offerings:
     - **ABORT IMMEDIATELY.** Do not launch subagents.
     - Instruct user to run `sales-setup <your-website-url>` to configure product DNA.

---

### Step 1 — Wave 1: Parallel Factual Gathering (Batch Launch)

1. Ensure the dedicated prospect scratchpad folder exists: `.agents/.scratchpad/{slug}/`.
2. Launch the 3 Wave 1 factual subagents in a **single parallel batch** call using `invoke_subagent`:
   - Subagent `sales-sub-company`:
     - Role: Firmographics, financials, tech stack, growth indicators
     - Output: `.agents/.scratchpad/{slug}/w1-company.md`
   - Subagent `sales-sub-contacts`:
     - Role: Buying committee mapping, decision-makers, email patterns
     - Output: `.agents/.scratchpad/{slug}/w1-contacts.md`
   - Subagent `sales-sub-competitive`:
     - Role: Incumbent software stack, switching costs, capability gaps
     - Output: `.agents/.scratchpad/{slug}/w1-competitive.md`
3. **Synchronization Barrier:** Verify that all 3 files exist and are populated via `view_file` before proceeding to Wave 2:
   - Verify presence of `.agents/.scratchpad/{slug}/w1-company.md`
   - Verify presence of `.agents/.scratchpad/{slug}/w1-contacts.md`
   - Verify presence of `.agents/.scratchpad/{slug}/w1-competitive.md`

---

### Step 2 — Wave 2: Synthesis & Opportunity Strategy

1. Invoke the unified Wave 2 analyst subagent via `invoke_subagent`:
   - Subagent: `sales-sub-analyst`
   - Inputs read by analyst:
     - Factual files: `w1-company.md`, `w1-contacts.md`, `w1-competitive.md`
     - Context files: `.agents/context/product-context.md`, `.agents/context/customer-context.md`, `.agents/context/scoring.md`, `.agents/context/output-formatting.md`
   - Analytical Tasks:
     - Calculate deterministic BANT score (0–100) and MEDDIC completeness (0–100%).
     - Compute composite Prospect Score and Tier classification.
     - Formulate personalized outreach strategy and A-R-C objection playbook.
   - Output produced: `.agents/.scratchpad/{slug}/w2-draft.md`
2. Confirm `.agents/.scratchpad/{slug}/w2-draft.md` is generated via `view_file`.

---

### Step 3 — QA Gate & Circuit Breaker (1 Retry Max)

1. Invoke the independent auditor subagent via `invoke_subagent`:
   - Subagent: `sales-sub-reviewer`
   - Target audited: `.agents/.scratchpad/{slug}/w2-draft.md`
   - Audit criteria (The 3 Invariants):
     - Invariant 1: Zero Hallucination (every claim traceable to `w1-*.md`)
     - Invariant 2: Product & Commercial Conformity (`.agents/context/product-context.md`)
     - Invariant 3: Mathematical Scoring Rigor (`.agents/context/scoring.md`)

2. **Verdict Evaluation & Circuit Breaker:**
   - **Case A (`VERDICT: APPROVED`):**
     - Audit passed cleanly. Proceed directly to Step 4.
   - **Case B (`VERDICT: REVISE REQUIRED`):**
     - **Circuit Breaker Triggered (Maximum 1 revision cycle):**
     - Re-invoke `sales-sub-analyst` with the exact itemized feedback from `sales-sub-reviewer`.
     - Analyst corrects the discrepancies and overwrites `.agents/.scratchpad/{slug}/w2-draft.md`.
     - Proceed immediately to Step 4 after this single correction pass (looping more than once is strictly forbidden).

---

### Step 4 — Publication & Deferred Dual Output

1. **Promote Machine-Readable Markdown:**
   - Write `.agents/.scratchpad/{slug}/w2-draft.md` content strictly to `reports/{slug}/markdown/PROSPECT-ANALYSIS.md` via `write_to_file`.
2. **Generate Interactive HTML Deliverable:**
   - Read `.agents/rules/references/report-template.html` via `view_file`.
   - Populate template placeholders with verified facts, scoring gauges, and strategy sections formatted according to `.agents/context/output-formatting.md`.
   - Write output strictly to `reports/{slug}/PROSPECT-ANALYSIS.html` via `write_to_file`.
3. **Scratchpad Housekeeping:**
   - Remove ephemeral intermediate files in `.agents/.scratchpad/{slug}/` to maintain workspace hygiene.
4. **User Delivery:**
   - Present executive briefing card and clickable local report links in the final conversation message.
