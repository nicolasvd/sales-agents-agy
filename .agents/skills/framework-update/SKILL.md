---
name: framework-update
description: >-
  Declarative workspace update and synchronization skill. Aligns skills, rules, and templates with upstream GitHub releases via REST API while strictly sanitizing and preserving user intelligence in the sanctuary denylist.
---

# Skill: framework-update

**Role:** Autonomous system maintenance and workspace synchronization engine.  
**Mode:** Interactive Human-in-the-Loop (inspection, changelog presentation, delta review, and explicit confirmation before file writing).  
**Mandatory Configuration:** `framework.json` (at workspace root).  
**Strict Guardrail:** Absolute zero shell commands, zero `curl`, zero `git merge`, zero `run_command`. All actions execute declaratively via native Antigravity tools (`read_url_content`, `view_file`, `write_to_file`).

> [!IMPORTANT]
> **Technical Governance:** Internal reasoning, GitHub REST API queries, changelog extraction, and terminal logs operate strictly in English.

---

## Triggers & Invocations

- `update`
- `update framework`
- `framework-update`

---

## Safeguards & Path Governance

### 1. Absolute Denylist (Sanctuary — Zero Mutation Guarantee)
The following paths and patterns are strictly sanctuarized. Under no circumstances may they be modified, overwritten, or deleted by an update:
- `reports/**` (all generated HTML, Markdown, and custom prospect dossiers)
- `*scratchpad/**` (all ephemeral and persisted analysis scratchpads)
- `.agents/rules/product-context.md` (Company DNA & offering rules)
- `.agents/rules/customer-context.md` (Target ICP & persona definitions)

### 2. Updatable Allowlist
Only files matching the following paths are eligible for upstream synchronization:
- `.agents/skills/**` (all skills, instruction files, scripts, and references)
- `.agents/rules/references/**` (HTML templates, index templates, format references)
- `.agents/rules/scoring.md` (deterministic scoring rubrics)
- `.agents/rules/fact-checking.md` (verification and primary source rules)
- `.agents/rules/output-formatting.md` (terminal and deliverable standards)
- `AGENTS.md` (system manifest and command index)
- `.agents/skills.json` (skill registry)
- `framework.json` (version tracking metadata)

> [!NOTE]
> When an upstream release introduces new files or subdirectories within allowed paths (e.g., a new skill under `.agents/skills/` or a new template under `.agents/rules/references/`), the update engine automatically recognizes and creates them (`🟢 Added`).

---

## 5-Phase Workflow

### Phase 1: Local Inspection & Upstream Probe
1. Read `framework.json` at root via `view_file` to extract:
   - `version` (e.g., `1.1.0`)
   - `repository.owner` (e.g., `nicolasvd`)
   - `repository.name` (e.g., `sales-agents-agy`)
   - `repository.api_base`
   - `repository.raw_base`
2. Fetch the latest release metadata from GitHub REST API via `read_url_content`:
   `GET https://api.github.com/repos/{owner}/{repo}/releases/latest`
3. Extract `tag_name`, release `name`, `body` (Release Notes / Changelog), and `published_at`.
4. Normalize version tags (strip leading `v`, e.g., `v1.2.0` → `1.2.0`).
5. **Comparison:**
   - If local `version` matches upstream `tag_name`: Notify user that the workspace is already up to date with the latest release, display current version info, and exit gracefully without prompting.
   - If an update is available: Proceed to Phase 2.

### Phase 2: Remote Tree & Delta Evaluation (Rate-Limiting Optimization)
1. Fetch the remote Git tree recursively for the target tag via `read_url_content`:
   `GET https://api.github.com/repos/{owner}/{repo}/git/trees/{tag}?recursive=1`
2. Iterate through tree items (`tree[]` with `type: "blob"`):
   - **Check Sanctuary Denylist:** If item path matches any sanctuary pattern, mark as `🛡️ Preserved (Sanctuary)` and skip any download.
   - **Check Allowlist:** If item path does NOT match the Allowlist, skip item.
   - **Evaluate Local Existence:** Check if target path exists locally via `view_file`:
     - If file does not exist locally → Mark as `🟢 Added`.
     - If file exists locally → Mark as `🟡 Modified` for update.
3. Consolidate delta metrics (count of files added, modified, and preserved).

### Phase 3: Interactive Presentation & User Confirmation (Human-in-the-Loop)
Present a structured update proposal in chat:

1. **Release Overview:**
   - Current Version vs Target Version (e.g., `v1.1.0` → `v1.2.0`)
   - Release Name & Publication Date
2. **Official Changelog:**
   - Render the release `body` markdown in an expandable block or clear section.
3. **Proposed File Delta Table:**
   | Status | File Path | Category / Impact |
   |---|---|---|
   | `🟢 Added` | `.agents/skills/sales-example/SKILL.md` | New Skill |
   | `🟡 Modified` | `.agents/rules/scoring.md` | Core Rule Update |
   | `🛡️ Preserved` | `.agents/rules/product-context.md` | Sanctuary (Company DNA) |
   | `🛡️ Preserved` | `.agents/rules/customer-context.md` | Sanctuary (Target ICP) |
   | `🛡️ Preserved` | `reports/**` | Sanctuary (Generated Reports) |
4. **Mandatory Overwrite Warning:**
   > [!WARNING]
   > Any manual edits made directly to internal skills or HTML templates outside the protected context rules (`product-context.md`, `customer-context.md`) will be overwritten by upstream release defaults.
5. **Confirmation Gate:**
   - Explicitly request user approval in chat (e.g., *"Please confirm to proceed with the update: [confirm / cancel]"*).
   - **HALT execution** and wait for the user's explicit affirmation before performing Phase 4.

### Phase 4: Declarative Execution
Upon receiving explicit user confirmation:
1. For each file marked `🟢 Added` or `🟡 Modified`:
   - Download raw content via `read_url_content` from:
     `https://raw.githubusercontent.com/{owner}/{repo}/{tag}/{path}`
   - Write content to target file path using `write_to_file` (with `Overwrite: true`).
2. Update `framework.json` at root:
   - Set `"version"` to target release tag without leading `v`.
   - Write updated `framework.json` via `write_to_file`.

### Phase 5: Executive Briefing Card & Completion
Emit the final standardized Executive Briefing Card:

### 🚀 Framework Update Applied: v{old_version} → v{new_version}

> [!TIP]
> **Repository:** `{owner}/{repo}` | **Release Tag:** `{tag}`  
> **Status:** Operational & Up-to-date

| Dimension | Count | Details |
|---|---|---|
| **Files Updated** | **{count_modified + count_added}** | {count_modified} modified, {count_added} added |
| **Sanctuary Files Preserved** | **{count_preserved}** | Protected against overwrite |
| **Framework Version** | `v{new_version}` | Synced with upstream |

- **UI Refresh Recommendation (Conditional):**
  - Check whether any HTML templates under `.agents/rules/references/` (e.g., `index-template.html`, `context-template.html`, `radar-template.html`, `pipeline-summary-template.html`) were in the list of `🟢 Added` or `🟡 Modified` files during the update.
  - **If at least one template was updated:** append the following native Markdown callout directly below the Executive Briefing Card:
    > [!TIP]
    > Global UI templates were updated. Run `report` to refresh your portal, Company DNA, and pipeline views with the latest layout.
  - **If no templates were updated:** omit this callout entirely.
