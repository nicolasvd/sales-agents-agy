# Détail des Sections ICP — Protocole Complet

Lire via : view_file(".agents/skills/sales-icp/references/icp-sections-detail.md")

## Output Format

Write the complete ICP to `reports/my-company/markdown/ICP-FRAMEWORK.md`.

Structure the output file with these sections in order:

```markdown
---
slug: "my-company"
company: "[Business/Product Name]"
url: "[URL or Not publicly available]"
type: "icp"
date: "[date]"
target_segment: "[Primary Segment]"
fit_threshold: 70
---

# Ideal Customer Profile: [Business/Product Name]

> Generated on [date] | Based on: [brief description of the business]

## ICP Summary
[2-3 paragraph executive summary of who the ideal customer is]

## Firmographic Criteria
[Table format with criteria, ranges, rationale]

## Technographic Profile
[Tech stack requirements, sophistication level, integration needs]

## Behavioral Signals
[Observable behaviors, content consumption, community membership]

## Pain Point Map
[Ranked pain points with severity, manifestation, triggers]

## Budget Qualifiers
[Financial criteria, deal size, ROI expectations]

## Channel Strategy
[How to reach them, decision process, content preferences]

## Negative ICP (Who to Avoid)
[Disqualification criteria with explanations]

## ICP Scoring Rubric
[100-point scorecard with grade bands]

## Buyer Personas

### Persona 1: [Name]
[Full persona details]

### Persona 2: [Name]
[Full persona details]

### Persona 3: [Name] (if applicable)
[Full persona details]

## Prospecting Playbook
[Where to find them, search strategies, prioritization, timing]

## Competitive Context
[Brief competitive landscape, positioning, displacement scenarios]

## ICP Maintenance Guide
[When to review, what signals indicate the ICP needs updating]

---

*ICP built by AI Sales Team | Review and refine quarterly*
```

---

## ICP Maintenance Guidance

Include a brief section at the end of the output file that advises on ICP maintenance:

- **Review Cadence:** Recommend reviewing the ICP quarterly or after any major product change, pricing change, or market shift.
- **Update Triggers:** List specific events that should prompt an ICP review:
  - You close 3+ deals outside the current ICP parameters
  - You lose 3+ deals to the same competitor or objection
  - Your product adds a major new feature or enters a new market
  - Your pricing model changes significantly
  - A major competitor enters or exits the market
- **Feedback Loop:** After running `prospect <url>` on 10+ companies, review which scores correlated with actual deal outcomes. Adjust ICP criteria and scoring weights accordingly.
- **Version Control:** Encourage the user to date-stamp ICPs and keep previous versions for comparison.

---

## Quality Standards

- Every criterion must be SPECIFIC. No "medium-sized companies" -- use exact ranges.
- Every recommendation must be ACTIONABLE. No "leverage social selling" -- say exactly what to do.
- Every persona must feel REAL. Use specific language patterns, not corporate jargon.
- The scoring rubric must be USABLE. Someone with no context should be able to score a lead in under 5 minutes.
- Pain points must reflect the PROSPECT's perspective, not the seller's pitch.
- The negative ICP is as important as the positive ICP. Be thorough.
- Cite your reasoning. Explain WHY each criterion matters, not just WHAT it is.
- If the user's description doesn't specify something, make an informed inference based on the product type, market, and price point. State your assumption explicitly.
- Every section should include at least one concrete example to illustrate the guidance.
- Tables should be used wherever structured data is presented for easy scanning.
- The prospecting playbook should include actual search query strings, not just descriptions of what to search for.

---

## Important Rules

1. Do NOT ask more than one clarifying question. Work with what you have and state assumptions.
2. Do NOT produce generic advice. Every line should be specific to this particular business.
3. Do NOT skip any section. All 6 dimensions, negative ICP, scoring rubric, personas, and playbook are required.
4. Do NOT use filler content. Every sentence should add value.
5. The output file should be 300-400 lines of substantive content.
6. Write the file to disk using the Write tool. Confirm to the user what was written and where.
7. After writing, give the user a brief summary of the ICP highlights and suggest next steps (e.g., "Run `prospect <url>` to analyze a specific company against this ICP").
