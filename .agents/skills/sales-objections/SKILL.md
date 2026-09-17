---
name: sales-objections
description: >-
  Objection handling playbook generator. Compiles 10+ common sales objections (budget, timing, competitors, internal build) with empathetic acknowledge-and-reframe scripts and discovery follow-ups, saving OBJECTION-PLAYBOOK.md.
---

# Skill: sales-objections

**Role:** Generate tactical objection handling playbooks grounded in the A-R-C framework (Acknowledge, Reframe, Clarify).  
**Mandatory Rules:** `customer-context.md` (mandatory), `product-context.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/{slug}/OBJECTION-PLAYBOOK.html` and `reports/{slug}/markdown/OBJECTION-PLAYBOOK.md`.

> [!IMPORTANT]
> **Language Governance:** Internal objection categorization, positioning logic, and talk tracks operate in English. Deliverable scripts automatically adapt to the primary language of the target audience.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Explicit argument provided:** Use the prospect slug (`reports/{slug}/`).
2. **Omitted argument (`*`):** Analyze recent conversation history. If a prospect account is already active in the exchange, deduce and reuse its slug without prompting for confirmation.
3. **Complete absence of context:** STOP IMMEDIATELY. Write NO files to disk. Prompt the user clearly for clarification:
   > *"Which prospect account would you like to analyze? (e.g., `objections prospect-slug <topic>`)"*

> [!CAUTION]
> **Strict Prohibition:** Never create any deliverable directly at the root of `reports/`.

## Trigger

Invoked via `objections [prospect]* <topic>`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (core persona friction points and exclusion criteria) and `.agents/rules/product-context.md` (authorized commercial offering, pricing, proof points). Then inspect available workspace context strictly in Markdown:
- `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- `reports/{slug}/markdown/COMPETITIVE-INTEL.md`
- `reports/{slug}/markdown/LEAD-QUALIFICATION.md` (red flags and budget signals)
- `reports/{slug}/markdown/COMPANY-RESEARCH.md` (financial trajectory and stack)

## Workflow (4 Sequential Steps)

1. **Context Extraction:**
   - Detect industry-specific challenges, identified competitors, and financial qualification cues from existing Markdown reports.

2. **Categorized Objection Selection:**
   - Structure responses across 3 distinct levels:
     - **Universal Objections:** Budget ("too expensive"), Timing ("call back next quarter"), Authority ("not my decision"), Status Quo ("we're fine as is"), Build vs. Buy ("we'll build it internally").
     - **Sector-Specific Objections:** Regulatory compliance, integration complexity, industry adoption speed.
     - **Competitive Objections:** Direct comparisons against detected incumbent software tools.
   - Comprehensive script library: `view_file(".agents/skills/sales-objections/references/objection-library.md")`.

3. **A-R-C Talk Track Construction (Non-Manipulative Consultative Standard):**
   - For every objection, apply the 3-step conversational pattern:
     - **A — Acknowledge:** Validate the prospect's concern empathetically without conceding ground.
     - **R — Reframe (Challenger Angle):** Reposition the constraint as an opportunity, strategic risk, or compounding Cost of Inaction.
     - **C — Clarify (Diagnostic Question):** Conclude with a targeted, open-ended discovery question to deepen dialogue. STRICTLY FORBIDDEN to push for a closing or signature while an objection is active.

4. **Product Alignment:**
   - Explicitly tie each reframe to confirmed capabilities, case studies, or economic metrics documented in `product-context.md`.

## Strict Guardrails

- ❌ Never disparage a competitor by name — highlight architectural and functional differences objectively.
- ❌ Never invent features, SLAs, or capabilities absent from `product-context.md`.
- ✅ Empathy first, logic second: never argue or get defensive in objection talk tracks.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/OBJECTION-PLAYBOOK.html` using `view_file(".agents/rules/references/battle-card-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/OBJECTION-PLAYBOOK.md` using `view_file(".agents/skills/sales-objections/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
