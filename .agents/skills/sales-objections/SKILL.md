---
name: sales-objections
description: >-
  Objection handling playbook generator. Compiles 10+ common sales objections (budget, timing, competitors, internal build) with empathetic acknowledge-and-reframe scripts and discovery follow-ups, saving OBJECTION-PLAYBOOK.md.
---

# Skill: sales-objections

**Role:** Generate tactical objection handling playbooks grounded in the A-R-C framework (Acknowledge, Reframe, Clarify).  
**Mandatory Rules:** `product-context.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/OBJECTION-PLAYBOOK.html` and `reports/markdown/OBJECTION-PLAYBOOK.md` (or prospect-specific under `reports/{slug}/`).

> [!IMPORTANT]
> **Language Governance:** Internal objection categorization, positioning logic, and talk tracks operate in English. Deliverable scripts automatically adapt to the primary language of the target audience.

## Trigger

Invoked via `objections <topic>`. Inspect available workspace context:
- `reports/{slug}/PROSPECT-ANALYSIS.html` or `reports/{slug}/COMPETITIVE-INTEL.html` (if generated for a specific prospect)
- `.agents/rules/product-context.md` (authorized commercial offering, pricing, and proof points — mandatory)

## Workflow (4 Sequential Steps)

1. **Context Extraction:**
   - Detect industry-specific challenges, identified competitors, and financial qualification cues from workspace reports.

2. **Categorized Objection Selection:**
   - Structure responses across 3 distinct levels:
     - **Universal Objections:** Budget ("too expensive"), Timing ("call back next quarter"), Authority ("not my decision"), Status Quo ("we're fine as is"), Build vs. Buy ("we'll build it internally").
     - **Sector-Specific Objections:** Regulatory compliance, integration complexity, industry adoption speed.
     - **Competitive Objections:** Direct comparisons against detected incumbent software tools.
   - Comprehensive script library: `view_file(".agents/skills/sales-objections/references/objection-library.md")`.

3. **A-R-C Talk Track Construction:**
   - For every objection, apply the 3-step conversational pattern:
     - **A — Acknowledge:** Validate the prospect's concern empathetically without conceding ground.
     - **R — Reframe:** Reposition the constraint as an opportunity or strategic risk of inaction.
     - **C — Clarify:** Conclude with a targeted, open-ended discovery question to advance dialogue.

4. **Product Alignment:**
   - Explicitly tie each reframe to confirmed capabilities, case studies, or economic metrics documented in `product-context.md`.

## Strict Guardrails

- ❌ Never disparage a competitor by name — highlight architectural and functional differences objectively.
- ❌ Never invent features, SLAs, or capabilities absent from `product-context.md`.
- ✅ Empathy first, logic second: never argue or get defensive in objection talk tracks.

## Mandatory Dual Output

Save both deliverables simultaneously:
- Standard Workspace Hub: `reports/OBJECTION-PLAYBOOK.html` and `reports/markdown/OBJECTION-PLAYBOOK.md`.
- Prospect-Specific (if triggered for a slug): `reports/{slug}/OBJECTION-PLAYBOOK.html` and `reports/{slug}/markdown/OBJECTION-PLAYBOOK.md`.
1. **Web HTML (Humans):** Using `view_file(".agents/rules/references/report-template.html")`.
2. **Raw Markdown (AI Memory):** Using `view_file(".agents/skills/sales-objections/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory 3-link completion block:

```markdown
---
### 📁 Generated Deliverables
- 🌐 **Web / Print Version (Humans):** [OBJECTION-PLAYBOOK.html](reports/OBJECTION-PLAYBOOK.html)
- 📄 **Raw Machine Data (AI):** [OBJECTION-PLAYBOOK.md](reports/markdown/OBJECTION-PLAYBOOK.md)
- 📑 **Global Reports Portal:** [index.html](reports/index.html)
```
