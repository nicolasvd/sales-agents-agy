# Règle : Format des Sorties & Génération d'Artifacts

## Bloc Résumé Terminal (Obligatoire en début de toute réponse)

Ce bloc apparaît EN PREMIER dans la réponse, avant tout développement :

```
=== [NOM DU SKILL EN MAJUSCULES] : [NOM ENTREPRISE] ===

[SCORE PRINCIPAL] : [X]/100  Grade : [A/B/C/D]
[Sous-scores si applicable, ex: Budget: 18/25  Authority: 20/25]

Top Signaux :
  1. [Signal le plus fort — preuve factuelle entre parenthèses]
  2. [Signal 2 — source]
  3. [Signal 3 — source]

Red Flags :
  1. [Point de vigilance principal]
  2. [Point de vigilance secondaire si pertinent]

Action recommandée : [Phrase d'action concrète, une seule ligne]

Rapport Markdown → reports/{slug}/[NOM-DU-FICHIER.md]
Artifact HTML    → reports/{slug}/PROSPECT-ANALYSIS.html (si prospect)
```

## Organisation du Stockage & Conventions de Nommage

Tous les livrables sont archivés dans le répertoire `reports/` :
- **Par prospect :** `reports/{slug}/` où `{slug}` est le nom de domaine ou d'entreprise normalisé en minuscules (ex. `reports/socialsky/`).
- **Global / Pipeline :** direct sous `reports/` (ex. `reports/PIPELINE-SUMMARY.md`).

| Skill | Type | Fichiers output |
|---|---|---|
| `sales-qualify` | Prospect | `reports/{slug}/LEAD-QUALIFICATION.md` |
| `sales-research` | Prospect | `reports/{slug}/COMPANY-RESEARCH.md` |
| `sales-contacts` | Prospect | `reports/{slug}/DECISION-MAKERS.md` |
| `sales-prospect` | Prospect | `reports/{slug}/PROSPECT-ANALYSIS.md` **ET** `reports/{slug}/PROSPECT-ANALYSIS.html` |
| `sales-outreach` | Prospect | `reports/{slug}/OUTREACH-SEQUENCE.md` |
| `sales-followup` | Prospect | `reports/{slug}/FOLLOWUP-SEQUENCE.md` |
| `sales-prep` | Prospect | `reports/{slug}/MEETING-PREP.md` |
| `sales-proposal` | Prospect | `reports/{slug}/CLIENT-PROPOSAL.md` |
| `sales-competitors` | Prospect | `reports/{slug}/COMPETITIVE-INTEL.md` |
| `sales-icp` | Stratégie | `reports/IDEAL-CUSTOMER-PROFILE.md` |
| `sales-objections` | Stratégie | `reports/OBJECTION-PLAYBOOK.md` |
| `sales-report` | Pipeline | `reports/PIPELINE-SUMMARY.md` |

### Double Génération d'Artifacts pour `prospect <url>`
À l'issue de chaque audit `prospect <url>`, l'orchestrateur `sales-prospect` génère simultanément :
1. **Rapport Markdown :** `reports/{slug}/PROSPECT-ANALYSIS.md` (pour lecture rapide, grep et versioning).
2. **Artifact HTML autonome :** `reports/{slug}/PROSPECT-ANALYSIS.html`
   - Instancié à partir du template `.agents/rules/references/report-template.html`.
   - Inclut le CSS inline, les jauges SVG circulaires/barres, les badges de statut et les styles `@media print` A4.

### Opération de fichier
- Si le fichier n'existe pas → `create_file` (crée automatiquement les dossiers parents)
- Si le fichier existe déjà → `edit_file` (écraser la version précédente)

### Structure Standard du Rapport Markdown
```markdown
# [Titre] : [Nom de l'entreprise]
**Date :** [YYYY-MM-DD]  **URL :** [url analysée]
---
## Résumé Exécutif & Score
[Table des scores avec formule]
---
## [Sections analytiques — données tabulaires, sourcées]
---
## Recommandations & Actions
[Plan priorisé]
---
*Généré par AI Sales Team Antigravity — [date]*
*Sources : [liste des URLs et requêtes utilisées]*
```
