---
name: sales-proposal
description: >-
  Client proposal generator. Creates comprehensive commercial proposals including executive summary, problem statement, solution architecture, ROI metrics, timeline, and terms, saving CLIENT-PROPOSAL.md.
---


# Skill : sales-proposal

**Rôle :** Générer une proposition commerciale complète et personnalisée.
**Règles requises :** `product-context.md` (obligatoire), `output-formatting.md`.
**Output :** `CLIENT-PROPOSAL.md`

## Déclenchement

Invoqué par la commande `proposal <nom_client>`. Lire :
- `PROSPECT-ANALYSIS.md` ou `LEAD-QUALIFICATION.md` (contexte prospect)
- `DECISION-MAKERS.md` (destinataire et structure de décision)
- `IDEAL-CUSTOMER-PROFILE.md` (calibration de l'offre)
- `.agents/rules/product-context.md` (offre, prix, fonctionnalités — obligatoire)

## Workflow (3 étapes)

1. **Collecte des inputs** — Lire tous les rapports disponibles ci-dessus.
   Si un rapport manque : `search_web` + `read_url_content` pour combler les lacunes.

2. **Génération de la proposition** — Structure imposée (dans l'ordre) :
   - Résumé exécutif (1 page max, orienté valeur, pas fonctionnalités)
   - Analyse de situation (pain points confirmés, sources citées)
   - Solution proposée (référencer `product-context.md` strictement)
   - Périmètre et jalons
   - Timeline (réaliste, buffer inclus)
   - Investissement (grille tarifaire de `product-context.md` uniquement)
   - Projection ROI (basée sur les pain points identifiés, conservatrice)
   - Équipe et références clients (celles documentées dans `product-context.md`)
   - Prochaines étapes (3 actions concrètes avec dates proposées)
   Pour le template complet de chaque section :
   `view_file(".agents/skills/sales-proposal/references/proposal-template.md")`

3. **Séquence de relance** — Inclure 3 e-mails de suivi post-envoi (J+2, J+5, J+10).

## Contraintes

- ❌ Ne jamais citer un prix absent de `product-context.md`.
- ❌ Ne jamais promettre une fonctionnalité non documentée.
- ✅ ROI = conservateur. Toujours signaler les hypothèses.
- ✅ Résumé exécutif rédigé pour le C-level : chiffres d'abord, contexte ensuite.

## Output (Double Livrable Obligatoire)

Créer simultanément dans `reports/{slug}/` :
1. **Markdown :** `reports/{slug}/CLIENT-PROPOSAL.md` selon le template :
   `view_file(".agents/skills/sales-proposal/references/proposal-template.md")`
2. **HTML Autonome :** `reports/{slug}/CLIENT-PROPOSAL.html` selon le template :
   `view_file(".agents/skills/sales-proposal/references/proposal-template.html")`

Afficher le bloc résumé terminal en début de réponse et le **bloc de clôture avec liens cliquables** en fin de réponse (conforme à `output-formatting.md`).
