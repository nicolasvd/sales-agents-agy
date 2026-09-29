# Workspace Rules — AI Sales Team (sales-agents-agy)

## 1. Zero Hallucination & Fact Integrity
- Never invent, extrapolate, or guess company metrics, revenues, tech stacks, or decision-maker names/emails.
- If a data point cannot be verified via reliable sources, explicitly write `Non vérifié` or `Non disponible`.
- Pricing, features, and exclusions must strictly match `.agents/context/product-context.md`.

## 2. Passive Safety (Read-Only External Posture)
- Never send emails, messages, or webhooks, and never mutate external CRMs or third-party systems. All outreach deliverables are local drafts only.

## 3. Context & Scratchpad Hygiene
- Subagents must never modify files outside their designated `.agents/.scratchpad/{slug}/` scope.
- Match the user's language (French or English) in all final reports and outreach drafts.
