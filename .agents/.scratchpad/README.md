# Antigravity Scratchpad Specification & Architecture

Transient inter-agent buffer for multi-agent workflows orchestrated by `sales-prospect`.

> [!IMPORTANT]
> **Ephemeral Storage:** Files under `.agents/.scratchpad/{slug}/` (`w1-*.md`, `w2-draft.md`) are ephemeral session buffers ignored by Git. Coordination, reasoning, and synthesis schemas operate strictly in Markdown.

## Directory Structure

For each target prospect slug `{slug}`:

```text
.agents/.scratchpad/{slug}/
├── w1-company.md       # Firmographics, financials, stack, growth signals (sales-sub-company)
├── w1-contacts.md      # Buying committee, decision-makers, email patterns (sales-sub-contacts)
├── w1-competitive.md   # Incumbent tooling, switching costs, capability gaps (sales-sub-competitive)
└── w2-draft.md         # Deterministic scoring, account strategy & draft report (sales-sub-analyst)
```

## Lifecycle State Machine

1. **Scratchpad Initialization:** Directory created by `sales-prospect` (`.agents/.scratchpad/{slug}/`).
2. **Wave 1 (Parallel Research):** Subagents `sales-sub-company`, `sales-sub-contacts`, and `sales-sub-competitive` write their respective `w1-*.md` Markdown files.
3. **Synchronization Barrier:** Wave 2 triggers only after all 3 Wave 1 Markdown files are populated.
4. **Wave 2 (Analyst Synthesis):** `sales-sub-analyst` ingests Wave 1 files and `.agents/context/` rubrics, computes deterministic scores, and writes `w2-draft.md`.
5. **QA Gate Review:** `sales-sub-reviewer` inspects `w2-draft.md` in read-only mode against the 3 invariants (Zero Hallucination, Product Conformity, Mathematical Rigor).
6. **Publication & Cleanup:** Final reports promoted to `reports/{slug}/`, and the ephemeral scratchpad folder is purged.
