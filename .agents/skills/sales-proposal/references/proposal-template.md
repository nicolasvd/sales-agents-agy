# Commercial Client Proposal Template

This template serves as the scaffold for `reports/{slug}/markdown/CLIENT-PROPOSAL.md`.
Read via: `view_file(".agents/skills/sales-proposal/references/proposal-template.md")`

```markdown
---
slug: "[slug]"
company: "[Client Company Name]"
url: "[URL or Not publicly available]"
type: "proposal"
date: "[Date]"
client_contact: "[Client Contact], [Title]"
prepared_by: "[Your Contact], [Title]"
valid_until: "[Date + 30 days]"
investment_structure: "[Dynamic SaaS / Flat-fee / CPM / Tiered]"
estimated_roi: "[ROI ratio or payback period]"
---

## [Your Company Name] for [Client Company Name]

Prepared for: [Client Contact], [Title]
Prepared by: [Your Contact], [Title]
Date: [Date]
Valid Until: [Date + 30 days]

CONFIDENTIAL

---

## Executive Summary

[Full executive summary — 1 page]

---

## Situation Analysis

[Current state, opportunities, competitive context, key challenges]

---

## Proposed Solution

[Strategic framework, phased approach with activities and milestones]

---

## Scope of Work

[Deliverables, meeting cadence, response times, tools, exclusions, client responsibilities]

---

## Timeline

[Visual timeline with phases, milestones, key dates]

---

## Investment & Commercial Structure

[Commercial proposal aligned strictly with .agents/rules/product-context.md (e.g. usage-based, CPM, SaaS subscription, or tiered if relevant). Every package or tier explicitly paired with ROI math.]

---

## ROI Projection & Cost of Inaction (COI)

### Projected Financial Return
[Current vs. projected metrics, ROI calculation, assumptions]

### Cost of Inaction (COI)
[Quantification of the monthly/quarterly financial loss incurred by maintaining the status quo]
$$\text{Cost of Inaction (COI)} = (\text{Monthly Lost Pipeline or Efficiency Deficit}) \times \text{Delay Duration}$$

---

## Your Team

[Team member profiles]

---

## Case Studies

[2-3 case studies in Challenge-Solution-Results format]

---

## Next Steps

[Clear action items, contact information, validity date]

---

## Appendix: Follow-Up Sequence

### Day 0 — Proposal Delivery Email
**Subject**: [Subject line]
[Full email body]

### Day 2 — Walkthrough Offer
**Subject**: [Subject line]
[Full email body]

### Day 5 — Value-Add
**Subject**: [Subject line]
[Full email body]

### Day 7 — Direct Check-In
**Subject**: [Subject line]
[Full email body]

### Day 14 — Second Value-Add
**Subject**: [Subject line]
[Full email body]

### Day 21 — Soft Close
**Subject**: [Subject line]
[Full email body]
```

---

## Rules and Constraints

1. **This is a SALES document.** Every paragraph must move the reader closer to saying yes. If a sentence does not sell, inform, or build trust, remove it.
2. **Lead with their problems.** Sections 2 and 3 (Executive Summary and Situation Analysis) should make the client feel deeply understood BEFORE you present any solution.
3. **Anchor every price to ROI.** Never present a number in isolation. Always pair it with the value it generates. "$5,000/month" alone is a cost. "$5,000/month that generates $25,000 in new revenue" is an investment.
4. **Use the client's own language.** If the client said "we need more qualified meetings," use "qualified meetings" — not "marketing qualified leads" or "sales opportunities." Mirror their exact words throughout.
5. **Keep under 15 pages.** A 30-page proposal signals that you cannot prioritize. Be concise and impactful.
6. **Be specific.** "We will increase your revenue" is meaningless. "We project a 25-35% increase in qualified pipeline within 90 days based on results with [comparable client]" is credible.
7. **Dynamic Commercial Structure.** Commercial models must strictly adhere to `.agents/rules/product-context.md` (e.g., usage-based, CPM, tiered subscriptions, or bespoke contracts). Never force a rigid 3-tier model if the product uses custom or transactional pricing. Always include Cost of Inaction (COI).
8. **Include exclusions.** A proposal without exclusions invites scope creep. Be explicit about what is NOT included.
9. **Case studies must be relevant.** Irrelevant case studies are worse than none. Match the client's industry, size, or challenge as closely as possible.
10. **If previous analysis files exist**, incorporate all available data from `reports/{slug}/markdown/` (`PROSPECT-ANALYSIS.md`, `COMPANY-RESEARCH.md`, `LEAD-QUALIFICATION.md`, `COMPETITIVE-INTEL.md`, `MEETING-PREP.md`). Do not ask the user to repeat information already captured in upstream files.
11. **Follow-up emails are part of the proposal output.** Always generate the 6-email follow-up sequence alongside the proposal — proposal delivery without a follow-up plan is incomplete.
12. **Conservative projections build trust.** In the ROI section, the conservative estimate should be genuinely conservative. Overpromising destroys credibility when results come in.
