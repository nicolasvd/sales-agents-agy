# Output Template — OBJECTION-PLAYBOOK.md

## Output Format

Write the complete objection handling playbook to `reports/{slug}/markdown/OBJECTION-PLAYBOOK.md` with the following structure:

```markdown
---
slug: "[slug or topic]"
company: "[Prospect Company or Universal]"
url: "[URL or Not publicly available]"
type: "objections"
date: "[Date]"
industry: "[Industry]"
primary_framework: "A-R-C (Acknowledge, Reframe, Clarify) & FFR"
total_objections: 20
---

# Objection Handling Playbook: [Industry/Topic]

Generated: [Date]
Industry: [Industry]
Customized For: [Prospect company if applicable]

---

## Quick Reference: Objection Response Matrix

| # | Objection | Real Meaning | Best Framework | Key Response |
|---|-----------|-------------|----------------|--------------|
| 1 | Too expensive | Value not proven | A-R-C | Show ROI math |
| 2 | Happy with current | Status quo bias | FFR | Gap analysis offer |
[...continue for all 15...]

---

## Frameworks

### Feel-Felt-Found (FFR)
[Framework description and structure]

### Acknowledge, Reframe, Clarify (A-R-C)
[Framework description and structure]

---

## Universal Objections (1-15)

[Full scripts for each objection]

---

## Industry-Specific Objections (16-20)

[5 additional objections specific to the industry]

---

## Competitive Objections

[Battle card responses for top 3 competitors]

---

## Pricing Deep Dive

[5 pricing tactics with scripts]

---

## Objection Prevention Tactics

[5 prevention techniques with scripts and examples]

---

## Practice Guide

- Role-play scenarios for the 5 hardest objections
- Recording prompts for self-coaching
- Common mistakes to avoid
```

---

## Rules and Constraints

1. **Word-for-word scripts.** Every response must be ready to speak aloud or copy-paste into an email. No summaries, frameworks-only, or "something like this" approximations.
2. **Honest about weaknesses.** If a competitor genuinely has an advantage, acknowledge it. Credibility is more valuable than winning one argument.
3. **Never manipulative.** No high-pressure tactics, guilt trips, fear-mongering, or manufactured urgency. Respect the prospect as an intelligent professional.
4. **Customized to context.** If the user provides a specific prospect or industry, every response must be tailored to that context — not generic.
5. **Both frameworks for every objection.** Always provide both FFR and A-R-C (Acknowledge, Reframe, Clarify) versions so the salesperson can choose the one that fits the moment and their style.
6. **Follow-up questions are mandatory.** An objection response without a follow-up question leaves the conversation dead. Every response must continue the dialogue.
7. **Include walk-away criteria.** Real salespeople need to know when to stop pushing. Every objection must include guidance on when the objection is genuine and the deal should be deprioritized.
8. **Proof points must be specific.** "Customers love us" is not a proof point. "[Company Name] increased [metric] by [X%] in [timeframe]" is a proof point. If specific customer data is not publicly available, indicate `Not publicly available` — never invent fictitious client names or metrics.
9. **If previous analysis files exist** in `reports/{slug}/markdown/` (`PROSPECT-ANALYSIS.md`, `COMPANY-RESEARCH.md`, `LEAD-QUALIFICATION.md`, `COMPETITIVE-INTEL.md`), incorporate competitive intelligence, prospect challenges, and qualification data into the objection responses.
10. **Natural language.** Scripts should sound like a real human talking, not a sales robot. Use contractions, conversational transitions, and genuine empathy.
