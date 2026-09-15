---
name: sales-report
description: >-
  Sales pipeline reporting agent. Aggregates all prospect audits, qualifications, and research files in the workspace into a consolidated executive pipeline report in SALES-REPORT.md.
---


# Skill : sales-report

**Rôle :** Générer un rapport pipeline agrégé depuis tous les rapports du workspace.
**Règles requises :** `scoring.md`, `output-formatting.md`.
**Output :** `SALES-REPORT.md`

## Déclenchement

Invoqué par la commande `report` (sans argument). Ce skill agrège tous les fichiers
de rapports existants dans le workspace.

## Workflow (3 étapes)

1. **Inventaire des rapports** — Scanner le workspace pour tous les fichiers :
   `LEAD-QUALIFICATION.md`, `PROSPECT-ANALYSIS.md`, `COMPANY-RESEARCH.md`
   et tout autre rapport généré par les skills précédents.

2. **Extraction des métriques clés** — Pour chaque prospect :
   - Prospect Score / BANT total / Grade (A/B/C/D)
   - Signaux déclencheurs identifiés
   - Statut outreach (si `OUTREACH-SEQUENCE.md` disponible)
   - Prochaine action recommandée

3. **Rapport pipeline consolidé** — Structure imposée :
   - Résumé exécutif (total prospects, score moyen, répartition des grades)
   - Dashboard pipeline (tableau : prospect, score, grade, signal fort, action)
   - Distribution des scores (histogram textuel A/B/C/D)
   - Top 3 prospects prioritaires (avec justification)
   - Actions immédiates (cette semaine)
   - Statut outreach global
   - Santé du pipeline (ratios, tendances)
   - Focus de la semaine (recommandation priorisée)
   Template complet : `view_file(".agents/skills/sales-report/references/output-template.md")`

## Contraintes

- Ne jamais inventer un score ou une métrique non présents dans les rapports sources.
- Si aucun rapport disponible → créer un `SALES-REPORT.md` avec section "Pipeline vide".
- Rapport = snapshot à date. Mentionner la date de génération.

## Output

Créer (ou écraser) `SALES-REPORT.md` selon le template de référence.
