# Template: Product Context File Generator

Use this template to generate `.agents/rules/product-context.md`. The resulting file must remain strictly < 5,120 bytes.

```markdown
# Rule: Strict Product Context

> [!IMPORTANT]
> This rule is the absolute source of truth. Zero extrapolation regarding pricing, services, expertise, or delivery boundaries.
> **Language Directive:** Internal reasoning operates in English. Pitch verbatims and outreach content adapt to the target prospect's primary language.

## Offering Identification

**Commercial Name:** {{COMPANY_NAME}}  
**Profile:** {{COMPANY_PROFILE}}  
**Positioning:** {{POSITIONING_STATEMENT}}

## Value Proposition (Verbatim)

{{VALUE_PROPOSITION}}

## Official Pricing Grid (Base Daily Rate: {{BASE_DAILY_RATE}})

| Package | Format & Duration | Pricing (excl. tax) | Inclusions |
|---|:---:|:---:|---|
| **{{PACKAGE_1_NAME}}** | {{PACKAGE_1_FORMAT}} | **{{PACKAGE_1_PRICE}}** | {{PACKAGE_1_INCLUSIONS}} |
| **{{PACKAGE_2_NAME}}** | {{PACKAGE_2_FORMAT}} | **{{PACKAGE_2_PRICE}}** | {{PACKAGE_2_INCLUSIONS}} |
| **{{PACKAGE_3_NAME}}** | {{PACKAGE_3_FORMAT}} | **{{PACKAGE_3_PRICE}}** | {{PACKAGE_3_INCLUSIONS}} |

## Core Practice Pillars

- **{{PILLAR_1_TITLE}}:** {{PILLAR_1_DESC}}
- **{{PILLAR_2_TITLE}}:** {{PILLAR_2_DESC}}
- **{{PILLAR_3_TITLE}}:** {{PILLAR_3_DESC}}

## STRICTLY Excluded Scopes

- {{EXCLUSION_1}}
- {{EXCLUSION_2}}
- {{EXCLUSION_3}}

## Target Personas

- **Economic Buyer:** {{BUYER_TITLES}}
  * *Pain point:* {{BUYER_PAINS}}
- **Internal Champion:** {{CHAMPION_TITLES}}
  * *Pain point:* {{CHAMPION_PAINS}}

## Security & Operational Constraints

- **Absolute Passivity:** The system generates drafts and analysis reports only. Zero automated sending of emails or external API mutations.
- **Human-in-the-Loop:** All deliverables, proposals, and outreach sequences require explicit human review and approval prior to execution.
```
