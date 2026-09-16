# Template: Customer Context File Generator

Use this template to generate `.agents/rules/customer-context.md`. The resulting file must remain strictly < 5,120 bytes.

```markdown
# Rule: Customer Context & Ideal Customer Profile (ICP)

> [!IMPORTANT]
> This rule defines the target customer profile, segmentation boundaries, and qualification filters.
> **Language Directive:** Internal reasoning operates in English. Downstream deliverables and outreach copy adapt to the target prospect's primary language.

## Ideal Customer Profile (ICP) Overview

**Target Segment:** {{TARGET_SEGMENT}}  
**Maturity Stage:** {{MATURITY_STAGE}}  
**Geographic Footprint:** {{GEOGRAPHIC_FOOTPRINT}}

## Firmographic & Technographic Boundaries

| Dimension | Target Sweet Spot | Disqualification Threshold |
|---|---|---|
| **Headcount** | {{HEADCOUNT_SWEET_SPOT}} | {{HEADCOUNT_DISQUALIFICATION}} |
| **Revenue / Funding** | {{REVENUE_SWEET_SPOT}} | {{REVENUE_DISQUALIFICATION}} |
| **Tech Stack** | {{TECH_STACK_SWEET_SPOT}} | {{TECH_STACK_DISQUALIFICATION}} |
| **Operating Model** | {{OPERATING_MODEL_SWEET_SPOT}} | {{OPERATING_MODEL_DISQUALIFICATION}} |

## Buying Committee & Target Personas

### 1. Economic Buyer (Decision Maker)
- **Titles:** {{ECONOMIC_BUYER_TITLES}}
- **Strategic Priorities:** {{ECONOMIC_BUYER_PRIORITIES}}
- **Core Pains:** {{ECONOMIC_BUYER_PAINS}}

### 2. Internal Champion (Day-to-Day Catalyst)
- **Titles:** {{CHAMPION_TITLES}}
- **Strategic Priorities:** {{CHAMPION_PRIORITIES}}
- **Core Pains:** {{CHAMPION_PAINS}}

### 3. Technical & Governance Evaluator
- **Titles:** {{TECH_EVALUATOR_TITLES}}
- **Key Criteria:** {{TECH_EVALUATOR_CRITERIA}}

## Business Triggers & High-Leverage Buying Signals

- **{{TRIGGER_1_LABEL}}:** {{TRIGGER_1_DESC}}
- **{{TRIGGER_2_LABEL}}:** {{TRIGGER_2_DESC}}
- **{{TRIGGER_3_LABEL}}:** {{TRIGGER_3_DESC}}
- **{{TRIGGER_4_LABEL}}:** {{TRIGGER_4_DESC}}

## Strict Exclusions & Disqualification Rules

- **{{EXCLUSION_1_LABEL}}:** {{EXCLUSION_1_DESC}}
- **{{EXCLUSION_2_LABEL}}:** {{EXCLUSION_2_DESC}}
- **{{EXCLUSION_3_LABEL}}:** {{EXCLUSION_3_DESC}}
- **{{EXCLUSION_4_LABEL}}:** {{EXCLUSION_4_DESC}}
```
