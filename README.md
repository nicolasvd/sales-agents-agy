<p align="center">
  <img src="banner.svg" alt="AI Sales Team - Antigravity Native" width="100%" />
</p>

# AI Sales Team — Antigravity Native

[![Release](https://img.shields.io/badge/Release-v1.1.0-blue.svg?style=flat-square)](https://github.com/nicolasvd/sales-agents-agy/releases)
[![Runtime](https://img.shields.io/badge/Runtime-Google%20Antigravity%202.0-4285F4.svg?style=flat-square)](https://antigravity.google)
[![Architecture](https://img.shields.io/badge/Architecture-100%25%20Declarative-success.svg?style=flat-square)](#-hub--spoke-architecture--folder-structure)
[![Engine](https://img.shields.io/badge/Engine-Gemini%203-8E75C4.svg?style=flat-square)](#)
[![Dependencies](https://img.shields.io/badge/Dependencies-Zero%20(No%20Python%2FNode)-brightgreen.svg?style=flat-square)](#)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

> 🇬🇧 **English** | [🇫🇷 Français](README.fr.md)

100% declarative B2B sales intelligence platform engineered natively for **Google Antigravity (Standalone / v2.0)** and orchestrated by **Gemini 3**. It transforms verified public web data into end-to-end sales intelligence: 360° prospect audits, deterministic BANT/MEDDIC qualification, buying committee mapping, multi-channel outreach sequences, and business cases calculating the quantified Cost of Inaction.

---

## 🚀 Quickstart

### Path A: 30-Second Fast-Track (100% No-Code)

Zero technical setup, terminal commands, or runtime environments (`npm`, `pip`, `venv`) required.

1. **Download the Latest Release:** Navigate to the [Latest Release](https://github.com/nicolasvd/sales-agents-agy/releases/latest) page, download the **Source code (zip)** archive, unzip it, and **rename the folder** to your preferred company or project name (e.g., `my-sales-agency`, `growth-intelligence`).
2. **Open in Antigravity:** Open **Google Antigravity**, click **Projects (+)** > **Open Folder**, and select your renamed project folder.
3. **Calibrate Your Offering:** In the prompt bar, simply run:
   ```text
   setup my-company.com
   ```
   *The agent crawls your domain, extracts your value proposition and core personas, and prompts 2 short questions to confirm your pricing rules.*
4. **The Golden Browser Cockpit Rule:**
    - In your file explorer, navigate to the `reports/` folder.
    - Right-click **`reports/index.html`** > **Open with Google Chrome** (or your preferred browser).
    - **Pin this browser tab.**
    - Whenever an agent completes a task, hit **Cmd + R** (or **F5**) on this tab to refresh your cockpit and inspect the new deliverables.

### Path B: Developer Track (Terminal / CLI)

```bash
# Clone repository and enter workspace
git clone [https://github.com/nicolasvd/sales-agents-agy.git](https://github.com/nicolasvd/sales-agents-agy.git) my-sales-agency
cd my-sales-agency

# Launch Antigravity
agy
```

> [!TIP]
> **Zero Dependencies:** No Python or Node.js runtimes, no virtual environments, and no package managers (`pip`, `npm`, `venv`). All agents execute using native declarative Antigravity tools (`read_url_content`, `search_web`, `create_file`, `view_file`).

---

## ⚡ Unified 15-Command Index

The framework utilizes an intelligent context-resolution syntax `[prospect]*`:
* **Explicit Target:** `outreach https://target.com` immediately targets the provided URL.
* **Omitted Argument (`*`):** If an account is already active in the ongoing chat session, the agent continues seamlessly.
* **Zero Active Context:** The agent halts immediately and prompts for a prospect target, preventing orphan deliverable generation.

| Category | Command | Skill | Primary Deliverables (HTML + AI Markdown) | Commercial Focus |
|---|---|---|---|---|
| **Foundation** | `setup <url>` | `sales-setup` | `reports/my-company/company-dna.html` | Audits your website & calibrates pricing rules |
| **Foundation** | `update` | `framework-update` | Console / `.agents/` | Updates skills & verifies declarative rule integrity |
| **Foundation** | `icp [segment]*` | `sales-icp` | `reports/my-company/ICP-FRAMEWORK.html` | Defines Ideal Customer Profile & negative exclusions |
| **Market** | `radar [topic/event]` | `sales-radar` | `reports/radar/RADAR-DISCOVERY.html` | Scans trailing triggers (D-60) and future catalysts (D+90) |
| **Audit** | `prospect <url>` | `sales-prospect`| `reports/{slug}/PROSPECT-ANALYSIS.html` | 2-Wave 360° audit (firmographics, signals, strategy) |
| **Audit** | `qualify [prospect]*` | `sales-qualify` | `reports/{slug}/LEAD-QUALIFICATION.html` | BANT scoring (0–100) & MEDDIC completeness |
| **Audit** | `research [prospect]*`| `sales-research`| `reports/{slug}/COMPANY-RESEARCH.html` | 8-dimension firmographics & headcount trends |
| **Audit** | `contacts [prospect]*`| `sales-contacts`| `reports/{slug}/DECISION-MAKERS.html` | Buying committee personas & verified recent hooks (< 90d) |
| **Audit** | `competitors [prospect]*`| `sales-competitors`| `reports/{slug}/COMPETITIVE-INTEL.html` | Incumbent tech stack identification & Battle Cards |
| **Action** | `prep [prospect]*` | `sales-prep` | `reports/{slug}/MEETING-PREP.html` | 10-point meeting brief & SPIN discovery questions |
| **Action** | `outreach [prospect]*` | `sales-outreach`| `reports/{slug}/OUTREACH-SEQUENCE.html` | 5-touch omnichannel sequence + LinkedIn angles |
| **Action** | `followup [prospect]*` | `sales-followup`| `reports/{slug}/FOLLOWUP-SEQUENCE.html` | 5 high-value lifecycle follow-up cadences |
| **Action** | `proposal [prospect]*` | `sales-proposal`| `reports/{slug}/CLIENT-PROPOSAL.html` | Value proposal & quantified Cost of Inaction (COI) |
| **Action** | `objections [prospect]* <topic>` | `sales-objections` | `reports/{slug}/OBJECTION-PLAYBOOK.html` | Consultative objection handling via A-R-C framework |
| **Pipeline** | `report` | `sales-report` | `reports/pipeline/PIPELINE-SUMMARY.html` | Consolidated pipeline rollup & Master Hub refresh |

---

## 🏛️ Hub & Spoke Architecture & Folder Structure

Deliverables follow a sandboxed hierarchy: no orphan reports are written to the root of `reports/` except the master portal.

```text
my-sales-agency/
├── AGENTS.md                          ← Session entry point & rules matrix
├── .agents/
│   ├── skills.json                    ← 15 native Antigravity skill definitions
│   ├── .scratchpad/                   ← Ephemeral inter-agent state buffer (gitignored)
│   └── rules/                         ← Governance rules & strict constraints (< 5 KB)
│       ├── product-context.md         ← Commercial product truth (strict source of truth)
│       ├── customer-context.md        ← Target ICP boundaries & negative filters
│       ├── fact-checking.md           ← Source validation protocol
│       ├── scoring.md                 ← Deterministic BANT / MEDDIC scorecards
│       └── output-formatting.md       ← Dual Output standard & typed YAML specifications
└── reports/
    ├── index.html                     ← MASTER COCKPIT (Interactive Hub view)
    │
    ├── my-company/                    ← INTERNAL FOUNDATION: Product truth & ICP
    │   ├── company-dna.html           ← Visual value proposition card
    │   ├── ICP-FRAMEWORK.html         ← Target framework
    │   └── markdown/                  ← Machine context files
    │
    ├── radar/                         ← UPSTREAM MARKET INTEL: Signals & events
    │   ├── RADAR-DISCOVERY.html       ← Market opportunities and detected hooks
    │   └── markdown/
    │
    ├── pipeline/                      ← PIPELINE ROLLUP: Executive portfolio status
    │   ├── PIPELINE-SUMMARY.html      ← Pipeline health metrics & deal rollup
    │   └── markdown/
    │
    └── {prospect-slug}/               ← ISOLATED PROSPECT WORKSPACES (1 per account)
        ├── PROSPECT-ANALYSIS.html     ← Polished Light SaaS HTML deliverables
        ├── MEETING-PREP.html          ← Print-ready A4 styling (@media print)
        ├── CLIENT-PROPOSAL.html
        └── markdown/                  ← RAW MACHINE TWINS (Typed YAML Frontmatter)
            ├── PROSPECT-ANALYSIS.md
            └── ...
```

---

## 🎯 Dual Output Standard: Human HTML + AI Machine Memory

Every skill simultaneously produces two synchronized formats:
1. **Visual Reports (Humans):** Modern, interactive Light SaaS HTML deliverables with dynamic scorecards, `@media print` A4 optimization, and a standardized return button (`<a href="../index.html" class="btn-back">← Back to Portal</a>`).
2. **Machine Memory (AI):** Raw Markdown files with **typed YAML Frontmatter** (`prospect_score`, `bant_total`, `meddic_completeness_pct`, `key_contacts`, `trigger_events`). Downstream skills (`prep`, `proposal`, `followup`) ingest these raw files directly, preventing token waste and hallucinations.

---

## ⚖️ Cardinal Principles & Governance

1. **Zero Hallucination:** Rely strictly on verified public web data. Missing parameters are labeled `Not publicly available`.
2. **Absolute Passivity:** The system never transmits external messages or initiates outreach. Every output is a draft for human review (*Human-in-the-Loop*).
3. **Deterministic Arithmetic Scoring:** Qualification relies strictly on transparent rules documented in `scoring.md`. No arbitrary ratings.
4. **Consultative Sales Alignment:** Anti-spam, anti-pressure sales posture. Objections are addressed through the **A-R-C (Acknowledge, Reframe, Clarify)** framework to deepen discovery, strictly forbidding premature closing.

---

## 💡 Origin & Attribution

This project is inspired by the pioneering work of [Zubair Trabzada](https://github.com/zubair-trabzada) on [ai-sales-team-claude](https://github.com/zubair-trabzada/ai-sales-team-claude), originally developed for Anthropic's Claude Code.

**Architectural Distinction:** This repository represents a complete declarative re-architecture for **Google Antigravity 2.0**. It eliminates Python execution scripts in favor of native declarative skills, structured file-based memory, and Gemini 3 multi-agent orchestration.

---

## 📄 License

Distributed under the MIT License.
