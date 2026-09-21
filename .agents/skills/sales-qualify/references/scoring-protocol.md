# Detailed Scoring Frameworks — BANT & MEDDIC

> Official scoring rubrics are defined in `.agents/rules/scoring.md`.
> This file contains signal-by-signal collection queries and methodology.

## Phase 1: Data Collection

### 1.1 Primary Data Sources

Gather qualification signals from these sources. Use `read_url_content` for website pages and `search_web` for external data.

| Source | What to Extract | Qualification Relevance |
|--------|----------------|------------------------|
| **Pricing page** | Price points, tiers, enterprise tier, "Contact Sales" | Budget signals, deal size potential |
| **Careers page** | Open roles, department sizes, growth rate | Budget (hiring = spending), Need (roles reveal pain), Timeline (urgency of hiring) |
| **Job postings** | Required tools, skills, responsibilities | Tech stack, pain points, current solutions, budget for tools |
| **Blog / Resources** | Pain point topics, challenges discussed, industry trends | Need validation, problem awareness |
| **Case studies** | Problems solved, vendors used, results achieved | Need patterns, buying behavior, vendor preferences |
| **About page** | Company size, stage, mission, leadership | Authority mapping, budget signals |
| **Review sites (G2, Capterra)** | Reviews of their product, reviews they leave for other tools | Current tool satisfaction, switching signals |
| **Glassdoor** | Employee reviews mentioning tools, processes, problems | Internal pain points, culture around change |
| **LinkedIn** | Employee count growth, recent hires, leadership posts | Timeline signals, authority mapping, growth trajectory |
| **News / Press** | Funding, partnerships, expansions, challenges | Budget signals, timeline triggers, need amplifiers |
| **Social media** | Company posts, executive posts, engagement | Problem awareness, vendor sentiment, trigger events |
| **Competitor mentions** | References to competing solutions on their site or job posts | Current solutions, competitive landscape |

### 1.2 Signal Extraction Methodology

For each data source, extract signals using this approach:

1. **Fetch the source** using read_url_content or search_web
2. **Scan for keywords** related to each BANT and MEDDIC dimension
3. **Classify each signal** as Strong, Moderate, Weak, or Absent
4. **Record the evidence** (exact quote or paraphrase with source URL)
5. **Assign confidence level** (High, Medium, Low, Inferred)

**Confidence level definitions:**

| Confidence | Definition | Example |
|-----------|-----------|---------|
| **High** | Directly stated or clearly observable fact | Pricing page shows $499/mo enterprise tier |
| **Medium** | Reasonable inference from available data | 5 open engineering roles suggests growing tech team |
| **Low** | Indirect signal requiring interpretation | Blog post about "scaling challenges" suggests growing pains |
| **Inferred** | Educated guess based on company profile | Series B company likely has $500K+ annual software budget |

---

## Phase 2: BANT Framework Assessment

### Budget (0-25 points)

**What we are assessing:** Does this prospect have the financial capacity and willingness to purchase our solution?

**Signal detection:**

| Signal | Points | Confidence | Where to Find |
|--------|--------|-----------|---------------|
| Explicit budget mentioned (rare for public data) | 20-25 | High | RFPs, procurement portals |
| Recent funding round (Series A: +12, B: +16, C+: +20) | 12-20 | High | Crunchbase, press releases |
| Enterprise pricing tier on their own product | 10-15 | Medium | Their pricing page |
| Multiple paid SaaS tools visible in tech stack | 8-12 | Medium | Job posts, integration pages |
| Hiring for roles that use your product category | 10-15 | Medium | Job postings |
| Employee count suggests adequate budget (50+ employees) | 5-10 | Low | LinkedIn, About page |
| Cost-conscious signals (all free tools, tiny team) | 0-3 | Medium | Tech stack, team size |
| Recent layoffs or cost-cutting news | 0-5 | High | News, LinkedIn |

**Budget scoring rubric:**

| Score | Interpretation |
|-------|---------------|
| 20-25 | Strong budget signals. Recent funding or clear enterprise spend. High confidence. |
| 15-19 | Good budget indicators. Company size and tech spend suggest capacity. |
| 10-14 | Moderate signals. Budget likely exists but unconfirmed. |
| 5-9 | Weak signals. Budget is uncertain. May require creative pricing. |
| 0-4 | Poor budget signals. Early stage, cost-conscious, or financial distress. |

### Authority (0-25 points)

**What we are assessing:** Can we identify who makes the buying decision, and can we access them?

**Signal detection:**

| Signal | Points | Confidence | Where to Find |
|--------|--------|-----------|---------------|
| Economic buyer identified by name and title | 20-25 | High | Team page, LinkedIn |
| Org structure visible (clear hierarchy) | 10-15 | Medium | Team page, LinkedIn, org chart |
| Decision-making titles found (VP+, C-suite, Director) | 8-12 | Medium | Team page, LinkedIn |
| Buying committee roles identifiable | 12-18 | Medium | Org structure, LinkedIn |
| Procurement process visible (vendor portal, RFP process) | 5-10 | Medium | Website, job postings |
| Flat org / owner-operator (easy authority mapping) | 15-20 | High | Small team, founder-led |
| Complex enterprise structure (hard to navigate) | 3-8 | Low | Large company, many layers |
| No leadership info publicly available | 0-5 | Low | Insufficient data |

**Authority scoring rubric:**

| Score | Interpretation |
|-------|---------------|
| 20-25 | Clear buying authority identified. Direct path to decision maker. |
| 15-19 | Key stakeholders identified. Likely buying process understood. |
| 10-14 | Some authority figures found. Buying process partially mapped. |
| 5-9 | Limited authority visibility. Need discovery call to map. |
| 0-4 | Cannot identify decision makers from public data. |

### Need (0-25 points)

**What we are assessing:** Does this prospect have a problem that our solution solves, and are they aware of it?

**Signal detection:**

| Signal | Points | Confidence | Where to Find |
|--------|--------|-----------|---------------|
| Explicit pain point mentioned (blog, interview, social) | 20-25 | High | Blog, news, social media |
| Job posting for role that solves the problem your tool solves | 15-20 | High | Job postings |
| Negative reviews of their current solution | 12-18 | Medium | G2, Capterra, social media |
| Blog content about challenges you solve | 10-15 | Medium | Company blog |
| Competitor product mentioned in job posts | 10-15 | Medium | Job postings |
| Industry-wide pain point applicable to their segment | 5-10 | Low | Industry reports, news |
| Feature requests on their own product suggest internal needs | 8-12 | Low | Community forums, social |
| No visible pain signals | 0-5 | Low | Insufficient data |

**Need scoring rubric:**

| Score | Interpretation |
|-------|---------------|
| 20-25 | Clear, validated pain point. Prospect is actively seeking solutions. |
| 15-19 | Strong need indicators. Problem is real even if not explicitly stated. |
| 10-14 | Moderate need signals. Likely experiencing the problem. |
| 5-9 | Weak need signals. Problem may exist but is not a priority. |
| 0-4 | No visible need. Solution may be premature for this prospect. |

### Timeline (0-25 points)

**What we are assessing:** Is there urgency to buy? What is the likely timeframe for a decision?

**Signal detection:**

| Signal | Points | Confidence | Where to Find |
|--------|--------|-----------|---------------|
| RFP or vendor evaluation in progress | 22-25 | High | Procurement portals, news |
| Active hiring for role that would use your product | 15-20 | High | Job postings |
| Recent trigger event (funding, leadership change, expansion) | 12-18 | Medium | News, press releases |
| Budget cycle alignment (fiscal year start, Q4 budget) | 8-12 | Low | Industry norms, fiscal calendar |
| Contract renewal cycle (annual contracts up for renewal) | 8-12 | Low | Inferred from industry |
| Seasonal buying patterns for their industry | 5-10 | Low | Industry knowledge |
| Competitor dissatisfaction signals (recent negative reviews) | 8-12 | Medium | G2, social media |
| Rapid growth creating urgency | 10-15 | Medium | Hiring pace, funding, news |
| No urgency signals detected | 0-5 | Low | Insufficient data |

**Timeline scoring rubric:**

| Score | Interpretation |
|-------|---------------|
| 20-25 | Active buying process or immediate trigger event. Decision within weeks. |
| 15-19 | Strong urgency signals. Likely to act within 1-3 months. |
| 10-14 | Moderate urgency. Timeframe is 3-6 months. |
| 5-9 | Low urgency. Timeframe is 6-12 months or undefined. |
| 0-4 | No urgency detected. Long-term nurture candidate. |

### BANT Score Calculation

```
BANT Score = Budget + Authority + Need + Timeline
Range: 0-100
```

---

## Phase 3: MEDDIC Framework Assessment

### Metrics

**What we are assessing:** What business metrics does this prospect care about? What would success look like to them?

**Research approach:**
1. Check their homepage for metric claims ("We help companies achieve X")
2. Read case studies for the metrics they highlight
3. Check executive LinkedIn posts for KPIs they discuss
4. Review job postings for OKR/KPI mentions
5. Analyze their product to infer which metrics their customers care about

**Output format:**
- Primary metrics they likely care about (3-5)
- How your solution impacts those metrics
- Evidence and confidence level for each

### Economic Buyer

**What we are assessing:** Who holds the purse strings? Who gives final approval?

**Research approach:**
1. Check team/leadership page for C-suite and VP titles
2. Search LinkedIn for the company + titles like "VP of [relevant department]", "Head of [relevant area]"
3. For SMBs: founder/CEO is almost always the economic buyer
4. For mid-market: VP or Director level in the relevant department
5. For enterprise: May need multiple approvals (VP + Procurement + Legal)

**Output format:**
- Name and title of likely economic buyer
- Evidence for why this person is the economic buyer
- Alternative economic buyers if uncertain
- Confidence level

### Decision Criteria

**What we are assessing:** What factors will they use to evaluate solutions?

**Research approach:**
1. Check if they have published evaluation criteria (RFPs, vendor requirements)
2. Analyze their job postings for tool requirements and evaluation criteria
3. Look at their current tech stack for patterns (best-of-breed vs suite, cloud-first vs hybrid)
4. Read reviews they have left for other tools (what do they value?)
5. Check their industry for common evaluation criteria

**Output format:**
- Likely evaluation criteria ranked by importance
- Evidence for each criterion
- How your solution performs against each criterion

### Decision Process

**What we are assessing:** How does this company buy software/services?

**Research approach:**
1. Company size: Smaller = faster, simpler process. Larger = committees, procurement
2. Check for procurement portals, vendor registration pages
3. Look for compliance requirements (SOC2, GDPR, HIPAA mentions)
4. Check if they have a dedicated procurement or vendor management team
5. Analyze their existing tech stack for buying pattern (many tools = decentralized, few = centralized)

**Output format:**
- Estimated buying process (self-serve, single decision maker, committee, formal procurement)
- Estimated timeline for the process
- Key stakeholders likely involved
- Potential gates or blockers in the process

### Identify Pain

**What we are assessing:** What specific pain points does this prospect experience that we can solve?

**Research approach:**
1. Read job postings for pain-related language ("we need to fix", "improve our", "build out")
2. Check Glassdoor reviews for internal frustrations
3. Read their blog for problem-focused content
4. Search social media for complaints or challenges they post about
5. Look at their product reviews for internal process issues
6. Check industry forums for common pain points in their segment

**Output format for each pain point:**
- Pain point description
- Evidence (with source)
- Severity estimate (Critical / High / Medium / Low)
- Your solution's relevance to this pain
- Confidence level

### Champion

**What we are assessing:** Who could be our internal advocate? Who would push for our solution inside the company?

**Research approach:**
1. Look for mid-level managers in the department that would use your product
2. Find people who have used your product (or competitors) at previous companies
3. Identify people who post about problems your product solves
4. Look for people who recently joined in roles related to your solution area
5. Find people who engage with your company's content or competitors' content

**Output format:**
- Potential champion(s) with name, title, and reasoning
- Connection points (shared connections, communities, interests)
- Approach strategy for each potential champion
- Confidence level

### MEDDIC Completeness Score

Calculate the percentage of MEDDIC elements with at least medium confidence:

```
MEDDIC Completeness = (Elements with Medium+ Confidence / 6) * 100
```

| Completeness | Interpretation |
|-------------|---------------|
| 80-100% | Excellent qualification data. Well-positioned for engagement. |
| 60-79% | Good data. Some gaps to fill during discovery calls. |
| 40-59% | Moderate data. Need discovery call to fill gaps before advancing. |
| 20-39% | Limited data. Early stage research. More intelligence needed. |
| 0-19% | Insufficient data. May need different research approach or sources. |

---

## Phase 4: Synthesis and Scoring

### 4.1 Opportunity Quality Score (0-100)

Calculate the composite score:

```
Opportunity Quality Score = (
    BANT_Score * 0.50 +
    MEDDIC_Completeness * 0.30 +
    Urgency_Modifier * 0.20
)
```

**Urgency Modifier (0-100):**
- 80-100: Active buying process or major trigger event in last 30 days
- 60-79: Recent trigger event (last 90 days) or strong urgency signals
- 40-59: Moderate urgency (industry trends, gradual pain escalation)
- 20-39: Low urgency (nice-to-have, future planning)
- 0-19: No urgency detected

### 4.2 Lead Grade Assignment

| Grade | Score Range | Label | Recommended Action |
|-------|-----------|-------|-------------------|
| **A** | 75-100 | Sales Qualified Lead | Assign to senior rep. Initiate personalized outreach immediately. Multi-thread to buying committee. Prepare custom proposal. |
| **B** | 50-74 | Marketing Qualified Lead | Begin standard outreach sequence. Schedule discovery call. Gather more MEDDIC data. Nurture with relevant content. |
| **C** | 25-49 | Information Qualified Lead | Add to long-term nurture. Share thought leadership content. Monitor for trigger events. Re-qualify in 60-90 days. |
| **D** | 0-24 | Unqualified | Do not pursue actively. Add to awareness campaigns only. Re-evaluate if major changes occur (funding, leadership, growth). |

### 4.3 Buying Signals Summary

Compile all positive buying signals detected during analysis:

| Signal | Source | Strength | Relevance |
|--------|--------|----------|-----------|
| [signal description] | [where found] | Strong/Moderate/Weak | [how it relates to buying] |

### 4.4 Red Flags Summary

Compile all concerns or negative signals:

| Red Flag | Source | Severity | Mitigation |
|----------|--------|----------|------------|
| [flag description] | [where found] | High/Medium/Low | [how to address] |

### 4.5 Recommended Approach

Based on the qualification data, recommend the sales approach:

**For Grade A leads:**
- Direct executive outreach
- Lead with specific ROI calculation
- Reference their specific pain points and trigger events
- Prepare for a 2-4 week deal cycle

**For Grade B leads:**
- Educational outreach
- Lead with industry insights and best practices
- Build relationship before pitching
- Prepare for a 1-3 month deal cycle

**For Grade C leads:**
- Content nurture
- Share relevant resources without selling
- Set trigger-based re-engagement alerts
- Prepare for a 3-6 month warming period

**For Grade D leads:**
- Marketing awareness only
- Add to newsletter/blog distribution
- Monitor for qualification changes
- Do not invest individual sales rep time

---
