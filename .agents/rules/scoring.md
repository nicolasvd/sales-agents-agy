# Règle : Barèmes de Scoring Déterministes

## BANT — 100 points au total (25 pts par dimension)

### Budget (0–25 pts) — Capacité et volonté de dépense
| Signal détecté | Points |
|---|---|
| Financement C+ / IPO récent (< 18 mois) | +20 |
| Financement B récent (< 18 mois) | +16 |
| Financement A récent (< 18 mois) | +12 |
| Revenus récurrents confirmés (ARR mentionné) | +10 |
| Stack SaaS multi-outils confirmée | +8 |
| Recrutement actif dans la catégorie produit | +10 |
| Effectif > 200 | +6 |
| Effectif 50–200 | +4 |
| Signaux de réduction de coûts ou licenciements | −10 |

### Authority (0–25 pts) — Accès aux décideurs
| Signal détecté | Points |
|---|---|
| Acheteur économique identifié (nom + titre confirmés) | +20 |
| Organigramme C-suite / VP visible publiquement | +12 |
| Structure plate (fondateur = décideur unique) | +15 |
| Multiples couches d'approbation détectées | +5 |

### Need (0–25 pts) — Intensité du besoin
| Signal détecté | Points |
|---|---|
| Pain point explicite sur site ou blog (citation directe) | +20 |
| Offre d'emploi résolvant le problème adressé | +15 |
| Avis négatifs sur l'outil actuel (G2/Capterra) | +12 |
| Contenu de blog sur les défis de notre catégorie | +10 |
| Aucun signal de besoin détecté | 0 |

### Timeline (0–25 pts) — Urgence et déclencheurs
| Signal détecté | Points |
|---|---|
| Trigger event < 30 jours (funding, M&A, exec hire) | +20 |
| Trigger event 30–90 jours | +12 |
| Recrutement actif dans la catégorie | +15 |
| Croissance rapide (> 30%/an confirmée) | +10 |
| Aucun signal d'urgence | 0 |

## MEDDIC — Complétude (0–100%)

| Élément | Critère "Trouvé" (confiance ≥ Moyenne) |
|---|---|
| **M** etrics | KPIs métier avec valeurs cibles identifiés |
| **E** conomic Buyer | Nom + titre de l'acheteur budgétaire confirmé |
| **D** ecision Criteria | Facteurs d'évaluation mentionnés publiquement |
| **D** ecision Process | Processus d'achat cartographié (même informel) |
| **I** dentify Pain | Pain point spécifique et documenté par une source |
| **C** hampion | Ambassadeur interne potentiel identifié (nom ou rôle) |

`Complétude MEDDIC (%) = (Éléments à confiance Moyenne+ / 6) × 100`

## Formule Composite — Prospect Score

```
Prospect Score = (BANT × 0,50) + (MEDDIC% × 0,30) + (Urgency × 0,20)
```

**Urgency Modifier (0–100) :**
| Situation | Score |
|---|---|
| Achat actif en cours ou trigger < 30 j | 80–100 |
| Trigger < 90 j | 60–79 |
| Tendance de croissance sans urgence immédiate | 40–59 |
| Faible urgence | 20–39 |
| Aucun signal | 0–19 |

## Grille de Notation

| Score | Grade | Signification | Action |
|---|---|---|---|
| 75–100 | **A — SQL** | Sales Qualified Lead | Outreach immédiat, priorité max |
| 50–74 | **B — MQL** | Marketing Qualified Lead | Séquence standard + découverte |
| 25–49 | **C — IQL** | Interest Qualified Lead | Nurture, surveiller triggers |
| 0–24 | **D** | Non qualifié | Déprioritiser |
