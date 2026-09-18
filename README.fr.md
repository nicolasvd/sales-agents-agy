<p align="center">
  <img src="banner.svg" alt="AI Sales Team - Antigravity Native" width="100%" />
</p>

# AI Sales Team — Antigravity Native

[![Release](https://img.shields.io/badge/Release-v1.1.0-blue.svg?style=flat-square)](https://github.com/nicolasvd/sales-agents-agy/releases)
[![Runtime](https://img.shields.io/badge/Runtime-Google%20Antigravity%202.0-4285F4.svg?style=flat-square)](https://antigravity.google)
[![Architecture](https://img.shields.io/badge/Architecture-100%25%20Declarative-success.svg?style=flat-square)](#-architecture--arborescence-hub--spoke)
[![Engine](https://img.shields.io/badge/Engine-Gemini%203-8E75C4.svg?style=flat-square)](#)
[![Dependencies](https://img.shields.io/badge/Dependencies-Zero%20(No%20Python%2FNode)-brightgreen.svg?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

> 🇫🇷 **Français** | [🇬🇧 English](README.md)

Plateforme d'intelligence commerciale B2B 100 % déclarative conçue nativement pour **Google Antigravity (Standalone / v2.0)** et orchestrée par **Gemini 3**. Elle transforme des données web publiques vérifiées en stratégies de vente complètes : audits 360°, grilles BANT/MEDDIC déterministes, cartographies de comités d'achat, séquences d'approche multicanales et propositions chiffrant le coût de l'inaction.

---

## 🚀 Démarrage Rapide

### Option A : Parcours 30s Fast-Track (Profil Métier No-Code)

Aucun terminal, aucun environnement de développement (`npm`, `pip`, `venv`) ni serveur local n'est requis.

1. **Télécharger la Dernière Release :** Rendez-vous sur la page [Latest Release](https://github.com/nicolasvd/sales-agents-agy/releases/latest), téléchargez l'archive **Source code (zip)**, décompressez-la et **renommez le dossier** avec le nom de votre entreprise ou projet (ex: `cabinet-sales`, `growth-intelligence`).
2. **Ouvrir dans Antigravity :** Lancez **Google Antigravity**, cliquez sur **Projects (+)** > **Open Folder** et sélectionnez votre dossier.
3. **Calibrer l'Offre Commerciale :** Dans la barre d'instruction, lancez simplement :
   ```text
   setup mon-entreprise.com
   ```
   *L'agent analyse votre présence, extrait votre proposition de valeur et vos personas cibles, puis vous pose 2 questions courtes pour calibrer votre tarification.*
4. **La Règle d'Or du Cockpit (Sans Serveur) :**
   - Rendez-vous dans le dossier `reports/` de votre projet.
   - Clic droit sur **`reports/index.html`** > **Ouvrir avec Google Chrome** (ou votre navigateur favori).
   - **Épinglez cet onglet.**
   - À chaque analyse terminée par l'agent, un simple **Cmd + R** (ou **F5**) sur cet onglet actualise votre cockpit et affiche les nouveaux livrables.

### Option B : Parcours Développeur (Terminal / CLI)

```bash
# Cloner le dépôt et entrer dans le workspace
git clone https://github.com/nicolasvd/sales-agents-agy.git mon-projet-sales
cd mon-projet-sales

# Lancer Antigravity CLI
agy
```

> [!TIP]
> **Zéro Dépendance :** Aucun runtime Python ou Node.js à compiler, aucun gestionnaire de paquets (`pip`, `npm`, `venv`). Tous les agents s'exécutent exclusivement via les outils déclaratifs natifs d'Antigravity (`read_url_content`, `search_web`, `create_file`, `view_file`).

---

## ⚡ Répertoire des 15 Commandes Unifiées

Le framework applique une passerelle de contexte intelligente `[prospect]*` :
* **Avec cible explicite :** `outreach https://prospect.com` analyse immédiatement ce compte.
* **Sans cible (`*`) :** Si un compte est actif dans l'échange en cours, l'agent poursuit dessus de manière transparente.
* **Sans aucun contexte :** L'agent s'arrête net et demande l'URL cible sans jamais créer de fichier orphelin.

| Catégorie | Commande | Compétence | Livrable Principal (HTML + Markdown IA) | Rôle Commercial |
|---|---|---|---|---|
| **Socle** | `setup <url>` | `sales-setup` | `reports/my-company/company-dna.html` | Audite votre site et calibre la vérité produit / pricing |
| **Socle** | `update` | `framework-update` | Console / `.agents/` | Met à jour le framework et valide l'intégrité des règles |
| **Socle** | `icp [segment]*` | `sales-icp` | `reports/my-company/ICP-FRAMEWORK.html` | Modélise le profil client idéal et les règles d'exclusion |
| **Marché** | `radar [thème/salon]` | `sales-radar` | `reports/radar/RADAR-DISCOVERY.html` | Détecte les catalyseurs récents (J-60) et à venir (J+90) |
| **Audit** | `prospect <url>` | `sales-prospect`| `reports/{slug}/PROSPECT-ANALYSIS.html` | Audit 360° en 2 vagues (qualification, signaux, stratégie) |
| **Audit** | `qualify [prospect]*` | `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION.html` | Score BANT (0–100) et complétude MEDDIC |
| **Audit** | `research [prospect]*`| `sales-research`| `reports/{slug}/COMPANY-RESEARCH.html` | Diagnostic firmographique 8 dimensions & signaux RH |
| **Audit** | `contacts [prospect]*`| `sales-contacts`| `reports/{slug}/DECISION-MAKERS.html` | Cartographie du comité d'achat & ancres récentes (< 90j) |
| **Audit** | `competitors [prospect]*`| `sales-competitors`| `reports/{slug}/COMPETITIVE-INTEL.html` | Analyse de la stack en place et Battle Cards de combat |
| **Action** | `prep [prospect]*` | `sales-prep` | `reports/{slug}/MEETING-PREP.html` | Brief de rendez-vous en 10 points & questions SPIN |
| **Action** | `outreach [prospect]*` | `sales-outreach`| `reports/{slug}/OUTREACH-SEQUENCE.html` | Séquence 5 touches personnalisée & approche LinkedIn |
| **Action** | `followup [prospect]*` | `sales-followup`| `reports/{slug}/FOLLOWUP-SEQUENCE.html` | 5 scénarios de relance à forte valeur ajoutée |
| **Action** | `proposal [prospect]*` | `sales-proposal`| `reports/{slug}/CLIENT-PROPOSAL.html` | Offre commerciale avec chiffrage du Coût de l'Inaction |
| **Action** | `objections [prospect]* <thème>` | `sales-objections` | `reports/{slug}/OBJECTION-PLAYBOOK.html` | Traitement des objections selon le framework A-R-C |
| **Pilotage**| `report` | `sales-report` | `reports/pipeline/PIPELINE-SUMMARY.html` | Synthèse consolidée du pipeline et mise à jour du Hub |

---

## 🏛️ Architecture & Arborescence Hub & Spoke

Tous les livrables respectent un partitionnement étanche : aucun rapport orphelin n'est créé à la racine de `reports/` à l'exception de l'index central.

```text
mon-projet-sales/
├── AGENTS.md                          ← Registre d'instructions déclaratives
├── .agents/
│   ├── skills.json                    ← Définition des 15 compétences natives
│   ├── .scratchpad/                   ← Tampon d'orchestration éphémère (ignoré par Git)
│   └── rules/                         ← Règles de gouvernance & contraintes (< 5 Ko)
│       ├── product-context.md         ← Référentiel de votre offre (source de vérité absolue)
│       ├── customer-context.md        ← Critères d'éligibilité ICP et Anti-ICP
│       ├── fact-checking.md           ← Protocole de vérification des sources publiques
│       ├── scoring.md                 ← Barèmes arithmétiques déterministes BANT / MEDDIC
│       └── output-formatting.md       ← Spécifications Dual Output & métadonnées YAML
└── reports/
    ├── index.html                     ← PORTAIL MAÎTRE (Vue Hub interactive)
    │
    ├── my-company/                    ← SOCLE INTERNE : Notre offre & ICP
    │   ├── company-dna.html           ← Cockpit visuel de notre proposition de valeur
    │   ├── ICP-FRAMEWORK.html         ← Framework de ciblage
    │   └── markdown/                  ← Spécifications IA brutes
    │
    ├── radar/                         ← DÉTECTION AMONT : Veille & opportunités marché
    │   ├── RADAR-DISCOVERY.html       ← Signaux d'achat détectés sur le secteur
    │   └── markdown/
    │
    ├── pipeline/                      ← PILOTAGE AVAL : Reporting consolidé
    │   ├── PIPELINE-SUMMARY.html      ← Synthèse globale du portefeuille de comptes
    │   └── markdown/
    │
    └── {slug-du-prospect}/             ← DOSSIERS PROSPECTS ISOLÉS (1 dossier par compte)
        ├── PROSPECT-ANALYSIS.html     ← Rapports HTML stylisés Light SaaS
        ├── MEETING-PREP.html          ← Prêts pour l'impression A4 (@media print)
        ├── CLIENT-PROPOSAL.html
        └── markdown/                  ← JUMEAUX IA BRUTS (Frontmatter YAML typé)
            ├── PROSPECT-ANALYSIS.md
            └── ...
```

---

## 🎯 Double Livrable : Visualisation Humaine & Mémoire IA

Chaque compétence génère simultanément deux versions synchronisées :
1. **Livrable Web (Humain) :** Fichier HTML moderne (thème Light SaaS, cartes de scores interactives, bouton de retour au Hub `← Back to Portal`, mise en page imprimable A4).
2. **Mémoire Machine (IA) :** Fichier Markdown doté d'un en-tête **YAML Frontmatter typé** (`prospect_score`, `bant_total`, `meddic_completeness_pct`, `key_contacts`, `trigger_events`). Les compétences suivantes (`prep`, `proposal`, `followup`) lisent directement ces données brutes, éliminant tout risque d'amnésie ou de surconsommation de tokens.

---

## ⚖️ Principes Cardinaux & Déontologie

1. **Zéro Hallucination :** Données web publiques vérifiées uniquement. Toute donnée introuvable est formellement annotée `Non disponible publiquement`.
2. **Passivité Absolue :** Le framework n'envoie aucun message vers l'extérieur. Tout livrable est un document de travail soumis à validation humaine (*Human-in-the-Loop*).
3. **Scoring Déterministe :** Barèmes arithmétiques BANT (0–100) et MEDDIC appliqués mécaniquement selon `scoring.md`. Aucun score fantaisiste.
4. **Posture Vente Consultative :** Refus des tactiques agressives de spam. Le traitement des objections utilise exclusivement le modèle **A-R-C (Acknowledge, Reframe, Clarify)** pour approfondir la découverte, en excluant tout closing forcé.

---

## 💡 Origine & Remerciements

Ce projet s'inspire du concept original développé par [Zubair Trabzada](https://github.com/zubair-trabzada) dans [ai-sales-team-claude](https://github.com/zubair-trabzada/ai-sales-team-claude), conçu pour Claude Code.

**Différence d'architecture :** Ce dépôt est une ré-ingénierie déclarative complète pour **Google Antigravity 2.0**. Il élimine l'intégralité des scripts Python au profit des compétences déclaratives, d'une mémoire machine sur disque et de l'orchestration multi-agents Gemini 3.

---

## 📄 Licence

Projet open-source distribué sous licence MIT.
