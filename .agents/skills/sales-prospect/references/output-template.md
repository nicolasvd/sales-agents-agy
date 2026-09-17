# Output Template — PROSPECT-ANALYSIS.md

## Output Format: reports/{slug}/markdown/PROSPECT-ANALYSIS.md

Write the final machine deliverable to `reports/{slug}/markdown/PROSPECT-ANALYSIS.md` with this exact structure:

```markdown
---
slug: "[slug]"
company_name: "[Company Name]"
domain: "[domain]"
audit_date: "[YYYY-MM-DD]"
scoring:
  prospect_score: [0-100]
  lead_grade: "[A/B/C/D]"
  bant_total: [0-100]
  meddic_completeness_pct: [0-100]
primary_contacts:
  economic_buyer: "[Name or Not publicly available]"
  champion: "[Name or Not publicly available]"
competitive_context:
  incumbent_tools: ["[Tool 1]", "[Tool 2]"]
  switching_cost: "[Low/Medium/High]"
top_triggers:
  - "[Trigger 1 (< 90 days)]"
  - "[Trigger 2 (< 90 days)]"
---

# Prospect Analysis: [Company Name]
**URL:** [url]
**Date:** [current date]
**Company Type:** [detected type]
**Industry:** [detected vertical]
**Prospect Score: [X]/100 (Grade: [letter grade] — [label])**
**Confidence:** [High/Medium/Low/Very Low]

---

## Executive Summary

[3-5 paragraph summary for a sales leader. Lead with the Prospect Score and grade.
Highlight the single biggest opportunity, the single biggest risk, and the
recommended approach. Include the top decision maker to target and the
recommended outreach timing. End with a clear go/no-go recommendation
and expected deal timeline.]

---

## Prospect Snapshot

| Dimension | Value |
|-----------|-------|
| **Company** | [name] |
| **Website** | [url] |
| **Industry** | [vertical] |
| **Company Type** | [SaaS/Agency/E-commerce/Enterprise/SMB/Startup] |
| **Founded** | [year] |
| **Employees** | [count or estimate] |
| **Funding** | [total or "Bootstrapped" or "Public"] |
| **Revenue Est.** | [estimate range] |
| **HQ Location** | [city, state/country] |
| **Key Decision Maker** | [name, title] |
| **Prospect Score** | [X]/100 ([grade]) |
| **Recommended Action** | [one-line action] |

---

## Score Breakdown (Deterministic Formula)

$$\text{Prospect Score} = (\text{BANT} \times 0.50) + (\text{MEDDIC Completeness \%} \times 0.30) + (\text{Urgency Modifier} \times 0.20)$$

| Dimension | Raw Score | Weight | Contribution | Key Signal / Grounding |
|---|---|---|---|---|
| **BANT Total** | [X]/100 | 50% | [X.X] pts | Budget ([X]/25), Authority ([X]/25), Need ([X]/25), Timeline ([X]/25) |
| **MEDDIC Completeness** | [X]% | 30% | [X.X] pts | [X]/6 dimensions confirmed with Medium+ confidence |
| **Urgency Modifier** | [X]/100 | 20% | [X.X] pts | [Urgency situation and catalyst date] |
| **COMPOSITE PROSPECT SCORE** | **[X]/100** | **100%** | **[X]/100** | **Grade: [A/B/C/D] — [Classification]** |

---

## Company Profile

[Full company research findings from the sales-company subagent.
Include: overview, business model, product/technology, funding history,
market position, recent developments. Cite specific sources.]

---

## Decision Maker Map

### Buying Committee

| Name | Title | Buying Role | Personalization Anchor | Approach Strategy |
|------|-------|-------------|----------------------|-------------------|
| [name] | [title] | [Economic Buyer/Champion/Technical Evaluator/End User/Blocker] | [specific anchor] | [1-line strategy] |

### Org Chart (Text-Based)

```
[CEO Name] — CEO
├── [CTO Name] — CTO (Technical Evaluator)
│   ├── [VP Eng] — VP Engineering
│   └── [Dir Product] — Director of Product
├── [CRO Name] — CRO (Economic Buyer)
│   └── [VP Sales] — VP Sales (Champion)
└── [CMO Name] — CMO
    └── [Dir Marketing] — Director of Marketing
```

### Top 3 Priority Contacts

[Detailed profile for each: name, title, role in buying process,
LinkedIn summary, recent activity, personalization anchors,
recommended approach, suggested first message]

---

## Opportunity Assessment

### BANT Scorecard

| Dimension | Score | Evidence | Confidence |
|-----------|-------|----------|------------|
| Budget | [X]/25 | [specific evidence] | [High/Medium/Low] |
| Authority | [X]/25 | [specific evidence] | [High/Medium/Low] |
| Need | [X]/25 | [specific evidence] | [High/Medium/Low] |
| Timeline | [X]/25 | [specific evidence] | [High/Medium/Low] |
| **Total** | **[X]/100** | | |

### MEDDIC Assessment

| Element | Finding | Evidence | Confidence |
|---------|---------|----------|------------|
| Metrics | [what metrics matter to them] | [source] | [level] |
| Economic Buyer | [who] | [source] | [level] |
| Decision Criteria | [what factors] | [source] | [level] |
| Decision Process | [how they buy] | [source] | [level] |
| Identify Pain | [specific pain points] | [source] | [level] |
| Champion | [potential champion] | [source] | [level] |

### Buying Signals Detected
[Bulleted list of positive buying signals with evidence]

### Red Flags
[Bulleted list of concerns or risks with evidence]

---

## Competitive Landscape

### Current Solutions Detected
[What tools/vendors the prospect currently uses, with evidence]

### Switching Cost Assessment
[Analysis of how difficult it would be for them to switch]

### Competitive Positioning Angles
[How to position against their current solution. Key differentiators to emphasize.
Weaknesses of their current solution to highlight.]

---

## Recommended Outreach Strategy

### Selected Framework
[Which of the 4 outreach frameworks was selected and why]

### Channel Strategy
[Primary and secondary channels. LinkedIn + email timing.]

### Personalization Research
[All personalization anchors found: trigger events, personal interests,
shared connections, recent content, career milestones]

### Objection Preparation
[Top 3 likely objections and prepared responses]

---

## Prioritized Action Plan

### Immediate (Next 24-48 Hours)
1. [Specific action with details]
2. [Specific action with details]
3. [Specific action with details]

### Short-Term (Next 1-2 Weeks)
1. [Specific action with details]
2. [Specific action with details]
3. [Specific action with details]

### Long-Term (Next 1-3 Months)
1. [Specific action with details]
2. [Specific action with details]

---

## Ready-to-Send First Email

**To:** [Name], [Title] at [Company]
**Subject Line A:** [subject]
**Subject Line B:** [subject]

---

[Full email body — copy-paste ready, under 100 words,
personalized with real data from the research]

---

**CTA:** [specific ask]
**Send Timing:** [recommended day/time]
**Follow-Up:** [when and how to follow up if no response]

---

*Generated by AI Sales Team — Prospect 360° Engine*
```

---

## Terminal Output

In addition to the file, display a condensed scorecard in the terminal:

```
============================================
  PROSPECT ANALYSIS COMPLETE
============================================

Company:  [name] ([type])
Industry: [vertical]
URL:      [url]

Prospect Score: [X]/100 (Grade: [letter] — [label])
Confidence:     [High/Medium/Low]

Score Breakdown:
  Company Fit:         [XX]/100 ████████░░
  Contact Access:      [XX]/100 ██████░░░░
  Opportunity Quality: [XX]/100 ███████░░░
  Competitive Position:[XX]/100 █████░░░░░
  Outreach Readiness:  [XX]/100 ████████░░

Key Decision Maker: [Name], [Title]

Top 3 Opportunities:
  1. [opportunity]
  2. [opportunity]
  3. [opportunity]

Top 3 Risks:
  1. [risk]
  2. [risk]
  3. [risk]

Next Step: [single most important action]

Full report saved to: reports/{slug}/markdown/PROSPECT-ANALYSIS.md
============================================
```

**Bar chart rendering rules:**
- Each bar is 10 characters wide
- Score 0-10 = 1 filled block, 11-20 = 2 filled blocks, etc.
- Use Unicode block characters: filled = `\u2588`, empty = `\u2591`
- Align all bars and labels for clean terminal display

---

## Error Handling

### URL Unreachable
1. Try alternate URL formats (www/non-www, http/https)
2. If all fail, report error and stop: "Could not reach [url]. Please verify the URL and try again."
3. Do NOT generate a report based on zero data

### Subagent Failure
1. Log which subagent failed and why
2. Assign neutral score (50) for that category
3. Add a note in the report: "[Category] analysis unavailable — neutral score assigned"
4. Reduce overall confidence by one level
5. Continue with remaining subagent data

### Site Behind Authentication
1. Note what was publicly accessible
2. Analyze only the public pages
3. Add a note: "Site requires authentication. Analysis limited to publicly accessible pages."
4. Recommend manual review of gated content
5. Reduce confidence level accordingly

### Minimal Content Site
1. If fewer than 3 pages are accessible, note "Limited site content"
2. Supplement with search_web for external data (Crunchbase, LinkedIn, news)
3. Adjust confidence to Low or Very Low
4. Recommend additional manual research

---

## Cross-Skill Integration

- If `reports/{slug}/markdown/COMPANY-RESEARCH.md` exists, incorporate its findings instead of running company research from scratch
- If `reports/{slug}/markdown/DECISION-MAKERS.md` exists, incorporate its findings into the contact analysis
- If `reports/{slug}/markdown/LEAD-QUALIFICATION.md` exists, incorporate its findings into the opportunity assessment
- If `reports/{slug}/markdown/COMPETITIVE-INTEL.md` exists, incorporate its findings into the competitive landscape
- If `reports/{slug}/markdown/OUTREACH-SEQUENCE.md` exists, reference it in the outreach strategy section
- Suggest follow-up native commands: `outreach` for cold email/LinkedIn sequence, `prep` for meeting preparation, `proposal` for deal-specific proposal, `objections` for objection handling
