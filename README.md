<p align="center">
  <img src="banner.svg" alt="AI Sales Team - Antigravity Native" width="100%" />
</p>

# AI Sales Team — Antigravity Native

> 🇬🇧 **English** | [🇫🇷 Français](README.fr.md)

100% declarative B2B sales intelligence platform built natively for **Google Antigravity (Standalone / v2.0)** and powered by **Gemini 3**. It analyzes accounts, qualifies leads, maps buying committees, and formulates high-touch outreach cadences exclusively from public web data.

---

## 💡 Origin & Inspiration

This project draws inspiration from the pioneering concept developed by [Zubair Trabzada](https://github.com/zubair-trabzada) in [ai-sales-team-claude](https://github.com/zubair-trabzada/ai-sales-team-claude), originally crafted for Anthropic's Claude Code.

> [!NOTE]
> **Complete Architectural Redesign (Not a Code Fork):**
> This repository is a ground-up declarative re-engineering for **Google Antigravity 2.0** and **Gemini 3**. It completely removes Python runtimes, scripts, and package managers (`pip`/`venv`), replacing them with declarative Antigravity skills (`skills.json`), structured multi-agent coordination (`.agents/.scratchpad/`), and a standard **Dual Output** architecture (Human HTML + AI Markdown).

---

## 🚀 Getting Started

### Path A: Fast-Track (No-Code via Google Antigravity)

Zero technical setup or terminal required.

1. Open **Google Antigravity**.
2. **Prompt 1 (Workspace Initialization):** Paste into the Antigravity prompt bar:
   ```text
   Initialize and inspect this sales-agents-agy workspace. Confirm that .agents/rules/ and .agents/skills/ are loaded, verify CLI routing (sales, prospect, outreach), and confirm readiness.
   ```
3. **Prompt 2 (Offer Configuration - Acme Example):**
   ```text
   Update .agents/rules/product-context.md to reflect our company profile:
   - Company: Acme AI Automation Inc. [or your company name]
   - Core Offering: [e.g., Enterprise Workflow Automation & AI Ops]
   - Rates & Packages: [e.g., Daily Rate: 800 $, Discovery Audit: 1 500 $, Implementation Sprint: 4 500 $]
   - Target Roles: [e.g., COO, VP Operations, Founders]
   - Exclusions: [e.g., No custom mobile app dev, no cold spam]
   Keep the file strictly under 5 KB.
   ```
4. Launch your first 360° audit:
   ```text
   prospect https://target-company.com
   ```

### Path B: Developer Track (CLI / Git)

```bash
# Clone repository
git clone https://github.com/nicolasvd/sales-agents-agy.git
cd sales-agents-agy

# Inspect product context rules
cat .agents/rules/product-context.md
wc -c .agents/rules/product-context.md

# Launch Antigravity
agy
```

> [!TIP]
> **Zero Dependencies:** No `npm install`, no `pip install`, and no runtime scripts. All agents execute using native Antigravity tools (`read_url_content`, `search_web`, `create_file`, `view_file`).

---

## 📊 Exploration Portal: `reports/index.html`

Every audit generates two synchronized deliverables:
- **Visual Web Reports (Humans):** Formatted HTML in `reports/{slug}/` with print-ready A4 styling and interactive scorecards.
- **Raw Machine Data (AI):** Unformatted Markdown files stored in `reports/{slug}/markdown/` for AI context reuse.

Open `reports/index.html` in any browser to access the central dashboard, search accounts dynamically, and review qualification grades (A/B/C/D). Note: `reports/` is 100% local and excluded from Git tracking (`.gitignore`).

---

## 🏛️ Core Principles & Architecture

1. **Zero Hallucination:** Only verified public web data. Missing data is strictly labeled `Not publicly available`.
2. **Absolute Passivity:** The system never sends emails or external messages. All outputs are drafts for human review.
3. **Deterministic Scoring:** Mathematical BANT (0–100) and MEDDIC completeness scorecards apply mechanically per [`.agents/rules/scoring.md`](.agents/rules/scoring.md).
4. **Strict Product Truth:** All outreach and proposals adhere strictly to [`.agents/rules/product-context.md`](.agents/rules/product-context.md).

```
sales-agents-agy/
├── AGENTS.md                    ← Root session instructions & rules matrix
├── .agents/
│   ├── skills.json              ← Declarative skill registry (18 skills)
│   ├── .scratchpad/             ← Ephemeral inter-agent state buffer (gitignored)
│   └── rules/                   ← Modular governance rules
│       ├── product-context.md   ← Commercial truth (pricing, limits)
│       ├── fact-checking.md     ← Public source verification protocol
│       ├── scoring.md           ← BANT / MEDDIC arithmetic scorecards
│       └── output-formatting.md ← Dual Output & completion standards
└── reports/
    ├── index.html               ← Master visual pipeline dashboard (local)
    └── {slug}/                  ← Prospect reports (HTML + markdown/ subfolder)
```

---

## ⚡ Command Index

| Command | Skill | Deliverables |
|---|---|---|
| `prospect <url>` | `sales-prospect` | 2-Wave 360° Audit (`reports/{slug}/PROSPECT-ANALYSIS.html` + `markdown/`) |
| `qualify <url>` | `sales-qualify` | BANT (0–100) + MEDDIC (`LEAD-QUALIFICATION.html` + `markdown/`) |
| `research <url>` | `sales-research` | 8-Dimension Firmographics (`COMPANY-RESEARCH.html` + `markdown/`) |
| `contacts <url>` | `sales-contacts` | Buying Committee & Personas (`DECISION-MAKERS.html` + `markdown/`) |
| `competitors <url>`| `sales-competitors`| Tech Stack & Battle Cards (`COMPETITIVE-INTEL.html` + `markdown/`) |
| `outreach <prospect>`| `sales-outreach` | 5-Touch Cadence + LinkedIn (`OUTREACH-SEQUENCE.html` + `markdown/`) |
| `followup <prospect>`| `sales-followup` | Adaptive Follow-up Sequence (`FOLLOWUP-SEQUENCE.html` + `markdown/`) |
| `prep <url>` | `sales-prep` | 10-Point Meeting Brief (`MEETING-PREP.html` + `markdown/`) |
| `proposal <client>` | `sales-proposal` | Value Proposal & ROI Model (`CLIENT-PROPOSAL.html` + `markdown/`) |
| `icp <desc>` | `sales-icp` | Ideal Customer Profile (`reports/IDEAL-CUSTOMER-PROFILE.html` + `markdown/`) |
| `objections <topic>`| `sales-objections` | A-R-C Objection Playbook (`reports/OBJECTION-PLAYBOOK.html` + `markdown/`) |
| `report` | `sales-report` | Pipeline Summary & Hub Update (`reports/PIPELINE-SUMMARY.html` + `index.html`) |

---

## ⚖️ License

MIT License. Contributions and PRs welcome via semantic commit conventions (`feat:`, `fix:`).
