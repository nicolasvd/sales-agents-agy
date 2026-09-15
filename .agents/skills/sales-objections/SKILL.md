---
name: sales-objections
description: >-
  Objection handling playbook generator. Compiles 10+ common sales objections (budget, timing, competitors, internal build) with empathetic acknowledge-and-reframe scripts and discovery follow-ups, saving OBJECTION-PLAYBOOK.md.
---


# Skill : sales-objections

**Rôle :** Générer un playbook de gestion des objections commerciales.
**Règles requises :** `product-context.md` (obligatoire), `output-formatting.md`.
**Output :** `OBJECTION-PLAYBOOK.md`

## Déclenchement

Invoqué par la commande `objections <topic>`. Lire :
- `PROSPECT-ANALYSIS.md` · `COMPETITIVE-INTEL.md` (contexte concurrent)
- `.agents/rules/product-context.md` (offre et différenciateurs — obligatoire)

## Workflow (4 étapes)

1. **Collecte du contexte** — Lire les rapports disponibles. Identifier :
   - Le secteur du prospect (objections sectorielles spécifiques)
   - Les concurrents détectés (objections de comparaison)
   - Le budget signalé (objections tarifaires)

2. **Sélection des objections pertinentes** — 3 niveaux :
   - **Universelles** (budget, timing, concurrent, build vs buy, décideur absent, etc.)
   - **Sectorielles** (selon l'industrie du prospect)
   - **Concurrentielles** (vs outils actuels détectés)
   Pour la bibliothèque complète avec scripts :
   `view_file(".agents/skills/sales-objections/references/objection-library.md")`

3. **Structurer chaque réponse** — Pattern A-R-C :
   - **A**cknowledge : valider le point de vue sans céder
   - **R**eframe : repositionner l'objection comme une opportunité
   - **C**larify : question de découverte pour approfondir

4. **Intégrer les différenciateurs** — Lier chaque réponse aux atouts documentés
   dans `product-context.md`. Aucune extrapolation.

## Contraintes

- ❌ Ne jamais dénigrer un concurrent nommément — pointer les gaps fonctionnels.
- ❌ Aucune promesse de fonctionnalité non listée dans `product-context.md`.
- ✅ Chaque réponse : empathie d'abord, argument ensuite.

## Output

Créer `OBJECTION-PLAYBOOK.md` selon le template :
`view_file(".agents/skills/sales-objections/references/output-template.md")`
