---
name: sales-outreach
description: >-
  Cold outreach email and LinkedIn sequence generator. Designs highly personalized 5-touch omnichannel outreach sequences based on company triggers and pains, saving OUTREACH-SEQUENCE.md.
---

# Skill: sales-outreach

**Role:** Generate highly personalized 5-touch omnichannel outreach sequences (Email + LinkedIn) strictly grounded in verified public trigger events.  
**Mandatory Rules:** `product-context.md` (mandatory), `customer-context.md` (mandatory), `fact-checking.md`, `output-formatting.md`, `scoring.md`.  
**Deliverables:** `reports/{slug}/OUTREACH-SEQUENCE.html` and `reports/{slug}/markdown/OUTREACH-SEQUENCE.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, trigger extraction, and scoring operate in English. Message copy automatically adapts to the primary language of the audited prospect.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Explicit argument provided:** Use the prospect slug (`reports/{slug}/`).
2. **Omitted argument (`*`):** Analyze recent conversation history. If a prospect account is already active in the exchange, deduce and reuse its slug without prompting for confirmation.
3. **Complete absence of context:** STOP IMMEDIATELY. Write NO files to disk. Prompt the user clearly for clarification:
   > *"Which prospect account would you like to analyze? (e.g., `outreach prospect-slug`)"*

> [!CAUTION]
> **Strict Prohibition:** Never create any deliverable directly at the root of `reports/`.

## Trigger

Invoked via `outreach [prospect]*`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` (ICP persona pains) and `.agents/rules/product-context.md` (product offering), then inspect available workspace intelligence (prioritizing Markdown files over HTML):
- Primary: `reports/{slug}/markdown/PROSPECT-ANALYSIS.md`
- Contacts: `reports/{slug}/markdown/DECISION-MAKERS.md`
- Diagnostic & Stack: `reports/{slug}/markdown/LEAD-QUALIFICATION.md`, `reports/{slug}/markdown/COMPANY-RESEARCH.md`, `reports/{slug}/markdown/COMPETITIVE-INTEL.md`
- ICP Context: `reports/my-company/markdown/ICP-FRAMEWORK.md`

## Workflow (6 Sequential Steps)

1. **Upstream Context Ingestion:** Read existing Markdown files using `view_file`. Extract confirmed pains, buyer personas, tech stack gaps, and already verified triggers.
2. **Targeted Trigger Gap-Fill:** Check existing files for verified triggers (< 90 days). IF valid triggers are already documented, **DO NOT run redundant web searches**. Only execute `search_web` if triggers are missing or > 90 days stale. Taxonomy: `view_file(".agents/skills/sales-outreach/references/outreach-frameworks.md")`.
3. **Framework Selection:** Select the optimal pattern (Observation→Connection→Ask, Problem→Proof→Ask, Trigger Event, Mutual Connection) matching prospect maturity.
4. **5-Touch Sequence Drafting:**
   - Day 1: Email (Trigger hook + Pain bridge + Soft CTA)
   - Day 3: LinkedIn (Engage-first profile connection note < 300 chars)
   - Day 7: Email (Value proposition grounded in `product-context.md`)
   - Day 14: Email (Case study or relevant insight)
   - Day 21: Email (Graceful break-up touch)
5. **LinkedIn Strategy:** Craft tailored connection request (Day 0/3) and Day 10 message (if connection accepted, or LinkedIn InMail alternative).
6. **Outreach Readiness Scoring:** Score sequence readiness (0–100) per `scoring.md` criteria.

## Strict Guardrails

- ❌ Never draft an outreach sequence without at least one verified trigger event.
- ❌ Never mention features, capabilities, or pricing absent from `product-context.md`.
- ❌ Absolute passivity: all outputs are drafts for human review. Never send messages externally.
- ✅ Keep all cold emails strictly under 100 words with a single open-ended question CTA.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/OUTREACH-SEQUENCE.html` using `view_file(".agents/rules/references/outreach-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/OUTREACH-SEQUENCE.md` using `view_file(".agents/skills/sales-outreach/references/output-template.md")`.

Display the Executive Briefing Card (Modern Markdown) at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
