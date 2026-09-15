---
name: sales-followup
description: >-
  Follow-up sequence generator for engaged leads, stalled deals, or no-response situations across email, LinkedIn, and phone, saving FOLLOWUP-SEQUENCE.md.
---


# Skill : sales-followup

**Rôle :** Générer une séquence de relance pour leads engagés, deals stagnants ou sans réponse.
**Règles requises :** `product-context.md`, `output-formatting.md`.
**Output :** `FOLLOWUP-SEQUENCE.md`

## Déclenchement

Invoqué par la commande `followup <nom_prospect>`. Lire :
- `OUTREACH-SEQUENCE.md` (séquence initiale envoyée)
- `DECISION-MAKERS.md` (contacts relancés)

## Workflow (4 étapes)

1. **Collecte du contexte de relance** — Lire les rapports disponibles. Identifier :
   - Nombre de tentatives déjà faites
   - Dernier point de contact (date, canal, contenu)
   - Signal de réponse (ouverture, clic, réponse partielle, silence complet)

2. **Sélection du scénario** — 4 scénarios selon la situation :
   - **Scénario A** : Pas de réponse (série "breakup" en 3 touches)
   - **Scénario B** : Intérêt exprimé mais deal stagnant (nurture + urgence)
   - **Scénario C** : Objection soulevée (relance ciblée post-objection)
   - **Scénario D** : Champion identifié, budget non confirmé (multi-threading)
   Bibliothèque complète de scénarios + scripts :
   `view_file(".agents/skills/sales-followup/references/scenario-library.md")`

3. **Personnalisation** — Chaque relance = nouveau déclencheur ou nouvel angle.
   Jamais le même message reformulé.

4. **Séquence multi-canal** — Alterner email, LinkedIn DM, téléphone si données disponibles.

## Contraintes

- Maximum 3 relances sans réponse avant le "breakup email".
- CTA = question ouverte. Jamais de demande de réunion dès le premier message.
- ❌ Aucun contact sortant réel — brouillons uniquement.

## Output

Créer `FOLLOWUP-SEQUENCE.md` selon le template :
`view_file(".agents/skills/sales-followup/references/output-template.md")`
