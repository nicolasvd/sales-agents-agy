---
name: sales-sub-strategy
description: >-
  Sous-agent interne de sales-prospect. Génère la stratégie d'outreach personnalisée : canal, angles de message, déclencheurs et objections anticipées. Invoqué par start_subagent en Vague 2.
---

# Sous-Agent : Outreach Strategy (`sales-sub-strategy`)

**Rôle :** Canal d'outreach, angles de message, déclencheurs, objections anticipées.
**Poids dans le Prospect Score :** Outreach Readiness = 20%.
**Règles requises :** `product-context.md` (obligatoire), `output-formatting.md`.
**Invocateur :** `sales-prospect` (Vague 2 — après opportunity_data disponible).

## Input Reçu (Pattern Scratchpad)

**Avant toute action**, lire DEUX fichiers :
```
view_file(".agents/.scratchpad/prospect_{slug}.json")
view_file(".agents/rules/product-context.md")   ← OBLIGATOIRE
```
Vérifier que `meta.status == "opportunity_done"` avant de poursuivre.
Extraire : tous les champs `wave1.*` et `wave2.opportunity_data`.

## Protocole d'Exécution

> Ce sous-agent N'EFFECTUE PAS de nouvelles recherches web.
> Il synthétise les données Vague 1 + Vague 2a en recommandations actionnables.

### Étape 1 — Sélection du Canal Principal

Évaluer dans l'ordre de priorité :
1. **Introduction chaude** : Connexion mutuelle détectée → priorité absolue
2. **LinkedIn DM** : Décideur actif publiquement sur LinkedIn → haute priorité
3. **E-mail froid** : E-mail pattern confirmé → priorité standard
4. **Téléphone** : Numéro direct disponible + rôle approprié (Fondateur, Sales leader)

Justifier le choix du canal avec les données `contacts_data`.

### Étape 2 — Identification des 3 Déclencheurs Prioritaires

Sélectionner parmi `company_data.growth_signals` et `opportunity_data.bant.timeline.signals`
les 3 événements récents les plus exploitables pour personnaliser l'accroche.

### Étape 3 — Angle de Message Personnalisé

Construire un angle en 3 éléments :
1. **Accroche déclencheur** : Référence à un événement réel récent
2. **Pont douleur → valeur** : Lier le pain identifié à notre proposition de valeur (`product-context.md`)
3. **CTA minimal** : Question ouverte, pas d'engagement fort

Respecter strictement `product-context.md` : ne jamais promettre une fonctionnalité non listée.

### Étape 4 — Objections Probables (Top 3)

Identifier les 3 objections les plus probables basées sur :
- `competitive_data.switching_cost` → objection de migration
- `company_data.tech_stack` → objection de doublon
- `opportunity_data.bant.budget` → objection de budget

### Étape 5 — Scoring Outreach Readiness (0–20 pts)
| Signal | Points |
|---|---|
| Canal + e-mail confirmés | +8 |
| 3 déclencheurs récents identifiés | +6 |
| Angle de message construit | +4 |
| Champion interne identifié | +2 |

## Output — Écriture dans le Scratchpad

Écrire via `edit_file` dans `.agents/.scratchpad/prospect_{slug}.json` :
Champ : `wave2.strategy_data` + mettre à jour `meta.status` → `"wave2_complete"`

```json
{
  "primary_channel": "LinkedIn|Email|Phone|Warm intro",
  "primary_contact": {"name": "...", "title": "...", "reach": "..."},
  "top_triggers": ["Trigger 1", "Trigger 2", "Trigger 3"],
  "message_angle": {
    "hook": "...",
    "pain_to_value_bridge": "...",
    "cta": "..."
  },
  "likely_objections": ["Objection 1", "Objection 2", "Objection 3"],
  "outreach_score": 0,
  "sources": []
}
```
