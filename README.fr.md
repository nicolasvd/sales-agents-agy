<p align="center">
  <img src="banner.svg" alt="AI Sales Team - Antigravity Native" width="100%" />
</p>

# AI Sales Team — Antigravity Native

> [🇬🇧 English](README.md) | 🇫🇷 **Français**

Plateforme d'intelligence commerciale B2B 100 % déclarative conçue nativement pour **Google Antigravity (Standalone / v2.0)** et orchestrée par **Gemini 3**. Elle analyse les entreprises, qualifie les opportunités, cartographie les comités d'achat et formule des séquences d'outreach ultra-personnalisées à partir de données web publiques vérifiées.

---

## 💡 Origine & Inspiration

Ce projet s'inspire du concept novateur développé par [Zubair Trabzada](https://github.com/zubair-trabzada) dans [ai-sales-team-claude](https://github.com/zubair-trabzada/ai-sales-team-claude), initialement pensé pour Claude Code (Anthropic).

> [!NOTE]
> **Ré-architecture intégrale (ce projet n'est pas un fork de code) :**
> Ce dépôt est une refonte déclarative native complète pour **Google Antigravity 2.0** et **Gemini 3**. Il élimine l'ensemble des scripts Python, runtimes et gestionnaires de paquets (`pip`/`venv`) au profit des compétences déclaratives (`skills.json`), d'une coordination multi-agents structurée sur disque (`.agents/.scratchpad/`), et d'une restitution standardisée en **Double Livrable** (HTML interactif pour les humains + Markdown brut pour les IA).

---

## 🚀 Démarrage Rapide

### Option A : Parcours Fast-Track (Profil Métier No-Code)

Aucune compétence technique ni terminal requis.

1. Ouvrez l'application **Google Antigravity**.
2. Copiez et collez ce prompt unique directement dans la barre d'instruction d'Antigravity :
   ```text
   Clone and initialize https://github.com/nicolasvd/sales-agents-agy.git into my active workspace. Inspect AGENTS.md, configure my commercial offer in .agents/rules/product-context.md, and get ready to run sales prospect audits.
   ```
3. Renseignez vos paramètres commerciaux dans [`.agents/rules/product-context.md`](.agents/rules/product-context.md) (forfaits, taux journalier, profil client idéal).
4. Lancez votre premier audit 360° :
   ```text
   prospect https://nom-du-prospect.com
   ```

### Option B : Parcours Développeur (CLI / Git)

```bash
# Cloner le dépôt
git clone https://github.com/nicolasvd/sales-agents-agy.git
cd sales-agents-agy

# Lancer Antigravity
agy
```

> [!TIP]
> **Zéro Dépendance :** Aucun `npm install`, aucun `pip install` ni script d'exécution. Tous les agents fonctionnent via les outils natifs d'Antigravity (`read_url_content`, `search_web`, `create_file`, `view_file`).

---

## 📊 Portail d'Exploration : `reports/index.html`

Chaque analyse produit simultanément deux livrables :
- **Rapports Web Visuels (Humains) :** Fichiers HTML stylisés sous `reports/{slug}/` optimisés pour l'impression A4 (`@media print`) avec cartes de score interactives.
- **Données Brutes Machine (IA) :** Fichiers Markdown sous `reports/{slug}/markdown/` réutilisables comme contexte d'inférence direct.

Ouvrez `reports/index.html` dans n'importe quel navigateur pour accéder au tableau de bord central, filtrer les entreprises en temps réel et consulter les notes de qualification (A/B/C/D).

---

## 🏛️ Principes Cardinaux & Gouvernance

1. **Zéro Hallucination :** Données web publiques vérifiées uniquement. Toute donnée absente est notée `Non disponible publiquement`.
2. **Passivité Absolue :** Le système n'envoie aucun message sortant. Tous les livrables sont des brouillons destinés à la revue humaine.
3. **Scoring Déterministe :** Barèmes arithmétiques BANT (0–100) et complétude MEDDIC appliqués mécaniquement selon [`.agents/rules/scoring.md`](.agents/rules/scoring.md).
4. **Vérité Produit Stricte :** Tout argumentaire ou proposition commerciale respecte strictement [`.agents/rules/product-context.md`](.agents/rules/product-context.md).

```
sales-agents-agy/
├── AGENTS.md                    ← Point d'entrée de session & matrice de règles
├── .agents/
│   ├── skills.json              ← Registre déclaratif (18 compétences)
│   ├── .scratchpad/             ← Tampon d'état inter-agents (ignoré par Git)
│   └── rules/                   ← Règles modulaires de gouvernance
│       ├── product-context.md   ← Vérité commerciale (tarifs, limites)
│       ├── fact-checking.md     ← Protocole de vérification des sources
│       ├── scoring.md           ← Barèmes déterministes BANT / MEDDIC
│       └── output-formatting.md ← Standard Dual Output et blocs terminaux
└── reports/
    ├── index.html               ← Tableau de bord visuel central
    └── {slug}/                  ← Dossier prospect (HTML + sous-dossier markdown/)
```

---

## ⚡ Répertoire des Commandes

| Commande | Compétence | Livrables générés |
|---|---|---|
| `prospect <url>` | `sales-prospect` | Audit 360° en 2 vagues (`reports/{slug}/PROSPECT-ANALYSIS.html` + `markdown/`) |
| `qualify <url>` | `sales-qualify` | BANT (0–100) + MEDDIC (`LEAD-QUALIFICATION.html` + `markdown/`) |
| `research <url>` | `sales-research` | Analyse firmographique 8 dimensions (`COMPANY-RESEARCH.html` + `markdown/`) |
| `contacts <url>` | `sales-contacts` | Comité d'achat & décideurs (`DECISION-MAKERS.html` + `markdown/`) |
| `competitors <url>`| `sales-competitors`| Détection de stack & Battle Cards (`COMPETITIVE-INTEL.html` + `markdown/`) |
| `outreach <prospect>`| `sales-outreach` | Séquence 5 touches + LinkedIn (`OUTREACH-SEQUENCE.html` + `markdown/`) |
| `followup <prospect>`| `sales-followup` | Séquences de relance adaptatives (`FOLLOWUP-SEQUENCE.html` + `markdown/`) |
| `prep <url>` | `sales-prep` | Brief de réunion en 10 points (`MEETING-PREP.html` + `markdown/`) |
| `proposal <client>` | `sales-proposal` | Proposition de valeur & ROI (`CLIENT-PROPOSAL.html` + `markdown/`) |
| `icp <desc>` | `sales-icp` | Profil Client Idéal (`reports/IDEAL-CUSTOMER-PROFILE.html` + `markdown/`) |
| `objections <topic>`| `sales-objections` | Playbook d'objections A-R-C (`reports/OBJECTION-PLAYBOOK.html` + `markdown/`) |
| `report` | `sales-report` | Synthèse pipeline & mise à jour du Hub (`reports/PIPELINE-SUMMARY.html` + `index.html`) |

---

## ⚖️ Licence

Licence MIT. Contributions bienvenues via les conventions de commits sémantiques (`feat:`, `fix:`).
