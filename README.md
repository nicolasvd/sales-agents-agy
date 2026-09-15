# AI Sales Team — Antigravity Native

Système d'intelligence commerciale B2B déclaratif pour **Google Antigravity (Standalone / v2.0)**.
Conçu pour analyser des prospects, cartographier des comités d'achat, qualifier des opportunités et générer des stratégies d'outreach hyper-personnalisées sans aucune intervention manuelle de prospection réelle.

> **Inspiration :** Ce projet est un portage 100 % Antigravity-native déclaratif inspiré de [ai-sales-team-claude](https://github.com/zubair-trabzada/ai-sales-team-claude) par Zubair Trabzada.

---

## ⚡ Zéro Dépendance (100 % Déclaratif)

Ce workspace ne requiert **aucun runtime Python, aucune installation `pip`, aucun environnement virtuel (`venv`) ni binaire externe**.

L'orchestration repose exclusivement sur les capacités natives du modèle Gemini 3 et les outils intégrés d'Antigravity :
- `read_url_content` : Navigation et scraping de pages statiques (sites officiels, mentions légales, blogs, pages tarifs).
- `search_web` : Intelligence externe en temps réel (actualités, levées de fonds, recrutements, avis clients, signaux LinkedIn).
- `create_file` & `edit_file` : Génération des livrables Markdown et persistance de données de session.
- `start_subagent` : Délégation asynchrone aux sous-agents d'audit spécialisés.
- `view_file` : Chargement à la demande des contextes et références.

---

## 🏛️ Gouvernance & Règles Transversales

Le comportement du système est encadré de façon déterministe par des règles Markdown strictes découvertes automatiquement par le runtime Antigravity :

```
Sales-agents/
├── AGENTS.md                    ← Point d'entrée session (principes cardinaux, routing, dépendances)
└── .agents/
    ├── skills.json              ← Registre de découverte des 18 compétences actives
    ├── .scratchpad/             ← Espace mémoire tampon inter-agents (gitignored)
    └── rules/                   ← Règles transversales modulaires
        ├── product-context.md   ← Source de vérité de l'offre vendue (prix, fonctionnalités, limites)
        ├── fact-checking.md     ← Protocole web strict (zéro hallucination, fraîcheur, sources citées)
        ├── scoring.md           ← Barèmes déterministes BANT (0-100) + MEDDIC (%) + Prospect Score
        └── output-formatting.md ← Structure des blocs de synthèse et convention reports/{slug}/
```

### Principes Non-Négociables
1. **Zéro Hallucination :** Données publiquement vérifiées uniquement. Toute donnée absente est notée `Non disponible publiquement`.
2. **Passivité Absolue :** Le système n'envoie aucun email ni message sortant. Tous les livrables sont des brouillons destinés à la revue humaine.
3. **Scoring Déterministe :** Application stricte des barèmes de `scoring.md` sans extrapolation optimiste.
4. **Contexte Produit Strict :** Alignement absolu avec `.agents/rules/product-context.md`.

---

## 🧩 Architecture des Compétences (13 Skills + 5 Sous-Agents)

Le registre regroupe **18 compétences actives**, optimisées sous un budget strict (< 90 lignes par `SKILL.md`) avec déport des volumineux templates et matrices dans des sous-dossiers `references/` chargés à la demande.

### Compétences Utilisateur (13)
- **`sales`** : Orchestrateur principal et aiguillage de la CLI.
- **`sales-qualify`** : Qualification BANT et complétude MEDDIC.
- **`sales-research`** : Analyse firmographique approfondie sur 8 dimensions.
- **`sales-contacts`** : Cartographie du comité d'achat (décideurs, champions, gatekeepers).
- **`sales-prospect`** : Audit 360° complet avec calcul du Prospect Score (0-100).
- **`sales-outreach`** : Génération de séquence d'outreach cold omnicanal (5 touches).
- **`sales-followup`** : Séquences de relance multi-scénarios (silence, objections, stagnation).
- **`sales-prep`** : Brief de réunion commerciale en 10 sections clés.
- **`sales-proposal`** : Rédaction de proposition commerciale complète et chiffrée.
- **`sales-objections`** : Playbook interactif de traitement d'objections (méthode A-R-C).
- **`sales-icp`** : Modélisation du profil client idéal et scoring associé.
- **`sales-competitors`** : Détection de tech stack, switching costs et Battle Cards.
- **`sales-report`** : Consolidation du statut global du pipeline commercial.

### Sous-Agents Internes (`sales-sub-*`)
Utilisés exclusivement par l'orchestrateur `sales-prospect` :
- `sales-sub-company` : Firmographics, signaux financiers et tech stack.
- `sales-sub-contacts` : Identification des décideurs et patterns d'e-mails.
- `sales-sub-competitive` : Analyse de l'écosystème d'outils et opportunités de déplacement.
- `sales-sub-opportunity` : Scoring déterministe BANT + MEDDIC.
- `sales-sub-strategy` : Choix du canal optimal, angles d'accroche et déclencheurs.

---

## 🔄 Workflow `prospect <url>` (2 Vagues & Scratchpad)

L'audit complet d'un prospect s'exécute en **2 vagues séquentielles** coordonnées via un fichier d'échange structuré sur disque : `.agents/.scratchpad/prospect_{slug}.json`.

```
                        prospect <url>
                              │
             [sales-prospect initialise le scratchpad]
                              │
       ┌──────────────────────┴──────────────────────┐
       │     VAGUE 1 : Recherche Indépendante        │
       │                                             │
       │  1. sales-sub-company                       │
       │  2. sales-sub-contacts                      │
       │  3. sales-sub-competitive                   │
       └──────────────────────┬──────────────────────┘
                              │
                [status = "wave1_complete"]
                              │
       ┌──────────────────────┴──────────────────────┐
       │     VAGUE 2 : Synthèse & Stratégie          │
       │                                             │
       │  4. sales-sub-opportunity (BANT / MEDDIC)   │
       │  5. sales-sub-strategy (Outreach & Angles)  │
       └──────────────────────┬──────────────────────┘
                              │
                [status = "wave2_complete"]
                              │
                              ▼
           reports/{slug}/PROSPECT-ANALYSIS.md
```

Ce pattern prévient la saturation du contexte mémoire (*attention dilution*) tout en assurant une traçabilité complète des données intermédiaires.

---

## 📁 Stockage des Livrables (`reports/`)

Tous les rapports générés sont automatiquement isolés et organisés sous le dossier `reports/` :

```text
reports/
├── .gitkeep
├── PIPELINE-SUMMARY.md                 ← Rapport consolidé multi-prospects
├── IDEAL-CUSTOMER-PROFILE.md           ← Livrable stratégique d'ICP
├── OBJECTION-PLAYBOOK.md               ← Playbook général de vente
└── {slug}/                             ← Dossier dédié par entreprise analysée
    ├── PROSPECT-ANALYSIS.md
    ├── LEAD-QUALIFICATION.md
    ├── COMPANY-RESEARCH.md
    ├── DECISION-MAKERS.md
    ├── OUTREACH-SEQUENCE.md
    ├── FOLLOWUP-SEQUENCE.md
    ├── MEETING-PREP.md
    ├── CLIENT-PROPOSAL.md
    └── COMPETITIVE-INTEL.md
```

---

## 🚀 Guide d'Usage

### 1. Configuration initiale du Produit
Renseigne `.agents/rules/product-context.md` avec tes données d'entreprise :
- Nom commercial, catégorie, proposition de valeur
- Grille tarifaire officielle et limites d'offres
- Personas cibles et différenciateurs concurrentiels

### 2. Lancement des Commandes

| Commande | Action | Livrable généré |
|---|---|---|
| `prospect <url>` | Audit 360° complet en 2 vagues | `reports/{slug}/PROSPECT-ANALYSIS.md` |
| `qualify <url>` | Qualification BANT/MEDDIC rapide | `reports/{slug}/LEAD-QUALIFICATION.md` |
| `research <url>` | Analyse firmographique détaillée | `reports/{slug}/COMPANY-RESEARCH.md` |
| `contacts <url>` | Cartographie du comité d'achat | `reports/{slug}/DECISION-MAKERS.md` |
| `outreach <prospect>` | Séquence de prospection 5 touches | `reports/{slug}/OUTREACH-SEQUENCE.md` |
| `followup <prospect>` | Séquence de relance ciblée | `reports/{slug}/FOLLOWUP-SEQUENCE.md` |
| `prep <url>` | Brief de préparation de réunion | `reports/{slug}/MEETING-PREP.md` |
| `proposal <client>` | Proposition commerciale complète | `reports/{slug}/CLIENT-PROPOSAL.md` |
| `competitors <url>` | Détection de stack & Battle Cards | `reports/{slug}/COMPETITIVE-INTEL.md` |
| `icp <description>` | Construction du persona & scoring ICP | `reports/IDEAL-CUSTOMER-PROFILE.md` |
| `objections <topic>` | Playbook de réponses aux objections | `reports/OBJECTION-PLAYBOOK.md` |
| `report` | Synthèse globale du pipeline | `reports/PIPELINE-SUMMARY.md` |

---

## 📜 Licence

Ce projet est distribué sous licence MIT. Consulter le fichier [LICENSE](LICENSE) pour plus de détails.
