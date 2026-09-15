---
name: sales-prep
description: >-
  Meeting preparation brief generator. Synthesizes prospect intelligence, key talking points, discovery questions, and tailored objection prep for upcoming sales calls, saving MEETING-PREP.md.
---


# Skill : sales-prep

**Rôle :** Générer un brief de préparation complet pour une réunion de vente.
**Règles requises :** `product-context.md`, `fact-checking.md`, `output-formatting.md`.
**Output :** `MEETING-PREP.md`

## Déclenchement

Invoqué par la commande `prep <url>`. Lire tous les rapports disponibles dans le workspace :
`PROSPECT-ANALYSIS.md`, `DECISION-MAKERS.md`, `LEAD-QUALIFICATION.md`, `COMPETITIVE-INTEL.md`

## Workflow (2 étapes)

1. **Phase de recherche** — Compléter les données manquantes :
   - `search_web` : actualité récente (< 30 jours) sur l'entreprise et les participants
   - `read_url_content` sur les pages non encore explorées
   - LinkedIn des participants via `search_web`

2. **Construction du brief** — 10 sections standardisées :
   1. Snapshot entreprise (2 min de lecture max)
   2. Profils des participants (titre, ancienneté, pain points probables)
   3. Situation business (contexte, enjeux actuels confirmés)
   4. Contexte concurrentiel (outils actuels, switching cost)
   5. Points de discussion clés (3 angles prioritaires)
   6. Questions de découverte (5 questions ouvertes SPIN/MEDDIC)
   7. Objections à anticiper (top 3, avec réponse préparée)
   8. Métriques de succès (comment mesurer le ROI de notre solution)
   9. Landmines concurrentielles (sujets à éviter)
   10. Prochaines étapes à proposer (2–3 options de next steps)
   Template complet de chaque section :
   `view_file(".agents/skills/sales-prep/references/meeting-brief-template.md")`

## Contraintes

- Questions de découverte = ouvertes, jamais orientées vers une vente.
- Produit présenté = strictement `product-context.md` (fonctionnalités + prix confirmés).
- Brief ≤ 2 pages (concis pour une lecture rapide avant la réunion).

## Output

Créer `MEETING-PREP.md` selon le template :
`view_file(".agents/skills/sales-prep/references/output-template.md")`
