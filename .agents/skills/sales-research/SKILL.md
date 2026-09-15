---
name: sales-research
description: >-
  In-depth company research and firmographics analysis. Evaluates business models, team size, financial signals, technology stack, and recent news, saving COMPANY-RESEARCH.md.
---


# Skill : sales-research

**Rôle :** Analyse firmographique approfondie d'un prospect B2B sur 8 dimensions.
**Règles requises :** `fact-checking.md`, `scoring.md`, `output-formatting.md`.
**Output :** `COMPANY-RESEARCH.md`

## Déclenchement

Invoqué par la commande `research <url>`.
Lire si disponible : `IDEAL-CUSTOMER-PROFILE.md`

## Workflow (4 étapes)

1. **Analyse du site officiel** — `read_url_content` sur 7 pages cibles :
   `/` → `/about` → `/pricing` → `/careers` → `/blog` → `/integrations` → `/customers`

2. **Recherche externe** — 5 requêtes `search_web` systématiques (cf. `fact-checking.md`) :
   - Funding & revenue
   - Effectifs & recrutement
   - News < 12 mois
   - Reviews G2/Capterra
   - Alternatives & concurrents

3. **Analyse sur 8 dimensions** — Pour chaque dimension, collecter les signaux et les sourcer :
   1. Vue d'ensemble (secteur, modèle, positionnement)
   2. Business model et revenus
   3. Produit et technologie
   4. Leadership et équipe
   5. Financement et santé financière
   6. Position marché
   7. Culture et employer brand
   8. Développements récents
   Protocole détaillé par dimension :
   `view_file(".agents/skills/sales-research/references/research-dimensions.md")`

4. **Synthèse et Company Fit Score** — Appliquer le barème Budget de `scoring.md`.

## Contraintes

- Chaque donnée = source entre parenthèses (Confirmé / Estimé / Non disponible).
- Données > 18 mois = étiquetées "historique".
- Ne jamais inférer un chiffre d'affaires non cité explicitement.

## Output

Créer `COMPANY-RESEARCH.md` selon le template :
`view_file(".agents/skills/sales-research/references/output-template.md")`
