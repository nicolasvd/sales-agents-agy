# Règle : Format des Sorties & Double Livrable (HTML Humains + MD IA)

## Bloc Résumé Terminal (Obligatoire en début de réponse)

Ce bloc apparaît EN PREMIER dans la réponse textuelle, avant tout développement :

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
```

## Organisation du Stockage : HTML pour Humains & MD pour IA

Pour chaque analyse, deux versions sont créées de façon étanche sous `reports/` :
- **Version Visuelle (Pour les Humains) :** Écrite directement dans `reports/{slug}/{LIVRABLE}.html`. Typographie soignée, composants interactifs, jauges SVG inline et styles d'impression A4 (`@media print`).
- **Version Données Brutes (Pour les IA) :** Rangée dans le sous-dossier `reports/{slug}/markdown/{LIVRABLE}.md` pour servir de contexte brut aux futurs agents ou prompts.
- **Portail Centralisé :** `reports/index.html` centralise et lie tous les livrables HTML générés.

| Skill | Version Web (Humains) | Version Brute (IA) | Template Référence |
|---|---|---|---|
| `sales-prospect` | `reports/{slug}/PROSPECT-ANALYSIS.html` | `reports/{slug}/markdown/PROSPECT-ANALYSIS.md` | `report-template.html` |
| `sales-outreach` | `reports/{slug}/OUTREACH-SEQUENCE.html` | `reports/{slug}/markdown/OUTREACH-SEQUENCE.md` | `outreach-template.html` |
| `sales-prep` | `reports/{slug}/MEETING-PREP.html` | `reports/{slug}/markdown/MEETING-PREP.md` | `meeting-prep-template.html` |
| `sales-proposal` | `reports/{slug}/CLIENT-PROPOSAL.html` | `reports/{slug}/markdown/CLIENT-PROPOSAL.md` | `proposal-template.html` |
| `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION.html` | `reports/{slug}/markdown/LEAD-QUALIFICATION.md` | `report-template.html` |
| `sales-research` | `reports/{slug}/COMPANY-RESEARCH.html` | `reports/{slug}/markdown/COMPANY-RESEARCH.md` | `report-template.html` |
| `sales-contacts` | `reports/{slug}/DECISION-MAKERS.html` | `reports/{slug}/markdown/DECISION-MAKERS.md` | `report-template.html` |
| `sales-competitors` | `reports/{slug}/COMPETITIVE-INTEL.html` | `reports/{slug}/markdown/COMPETITIVE-INTEL.md` | `report-template.html` |
| `sales-report` | `reports/PIPELINE-SUMMARY.html` | `reports/markdown/PIPELINE-SUMMARY.md` | `index-template.html` |

## Standard du Bloc de Clôture (Liens Cliquables Obligatoires)

Toute réponse d'un skill doit **IMPÉRATIVEMENT se terminer** par ce récapitulatif avec liens directs absolus :

```markdown
---
### 📁 Livrables Générés
- 🌐 **Version Web / Print (Humains) :** [NOM-DU-FICHIER.html](file://{ABSOLUTE_WORKSPACE_PATH}/reports/{slug}/NOM-DU-FICHIER.html)
- 📄 **Données Brutes (IA) :** [NOM-DU-FICHIER.md](file://{ABSOLUTE_WORKSPACE_PATH}/reports/{slug}/markdown/NOM-DU-FICHIER.md)
- 📑 **Portail Global des Rapports :** [index.html](file://{ABSOLUTE_WORKSPACE_PATH}/reports/index.html)
```

*(Où `{ABSOLUTE_WORKSPACE_PATH}` vaut `/Users/nicolasvd/antigravity/sales-agents-agy`)*.
