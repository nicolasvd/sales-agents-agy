---
name: framework-update
description: >-
  Declarative workspace update and synchronization skill. Aligns skills, rules, and templates with upstream GitHub releases via REST API while strictly sanitizing and preserving user intelligence in the sanctuary denylist.
---

# Skill: framework-update

**Role:** Autonomous system maintenance and workspace synchronization engine.  
**Mode:** Interactive Human-in-the-Loop (inspection, changelog presentation, delta review, and explicit confirmation before file writing).  
**Mandatory Configuration:** `framework.json` (at workspace root).  
**Strict Guardrail:** Absolute zero `curl`, zero `git merge`. All read/write operations execute declaratively via native Antigravity tools (`read_url_content`, `view_file`, `write_to_file`). `run_command` is permitted **exclusively** for file deletion (`rm`, `rmdir`) during the cleanup step in Phase 4 — no other shell commands are allowed.

> [!IMPORTANT]
> **Technical Governance:** Internal reasoning, GitHub REST API queries, changelog extraction, and terminal logs operate strictly in English.

---

## Triggers & Invocations

- `update`
- `update framework`
- `framework-update`
- `update --force` (forces delta evaluation & orphan cleanup even when already at latest version)
- `update clean` (alias for force cleanup of deprecated or orphan files)
- `repair` (alias to re-align workspace files with upstream release and purge legacy orphans)

---

## Safeguards & Path Governance

### 1. Absolute Denylist (Sanctuary — Zero Mutation Guarantee)
The following paths and patterns are strictly sanctuarized. Under no circumstances may they be modified, overwritten, or deleted by an update:
- `reports/**` (all generated HTML, Markdown, and custom prospect dossiers)
- `*scratchpad/**` (all ephemeral and persisted analysis scratchpads)
- `.agents/context/**` **excluding** `.agents/context/templates/**` (Company DNA, target ICP, scoring rubrics, and passive context — the templates subdirectory is updatable per the Allowlist below)

> [!IMPORTANT]
> **Precedence rule:** The Updatable Allowlist takes precedence over the Sanctuary Denylist for the `.agents/context/templates/**` path. Template files under that subdirectory are eligible for update and deletion by the engine; all other files under `.agents/context/` remain permanently sanctuarized.

### 2. Updatable Allowlist
Only files matching the following paths are eligible for upstream synchronization:
- `.agents/agents/**` (all agent definitions and orchestrator specifications)
- `.agents/skills/**` (all skills, instruction files, scripts, and references)
- `.agents/context/templates/**` (global HTML templates, design tokens, format references)
- `.agents/rules/fact-checking.md` (verification and primary source rules)
- `AGENTS.md` (system manifest and invariant workspace rules)
- `.agents/skills.json` (skill registry)
- `framework.json` (version tracking metadata)

> [!NOTE]
> When an upstream release introduces new files or subdirectories within allowed paths (e.g., a new skill under `.agents/skills/` or a new template under `.agents/context/templates/`), the update engine automatically recognizes and creates them (`🟢 Added`).

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
5. **Comparison & Force / Repair Evaluation:**
   - Detect invocation mode: check if the user triggered a forced re-alignment or repair (`update --force`, `update clean`, `repair`).
   - **When local `version` matches upstream `tag_name`:**
     - If a force/repair mode was requested: inform the user that the workspace version matches the latest release (`v{version}`), but proceed to Phase 2 to re-evaluate the tree, verify file integrity, and purge orphan or deprecated files.
     - Otherwise: notify user that the workspace is already up to date with the latest release (`v{version}`), display current version info, and exit gracefully without prompting.
   - **When an update is available (`local_version != upstream_tag`):** Proceed to Phase 2.

### Phase 2: Remote Tree & Delta Evaluation (Rate-Limiting Optimization)
1. Fetch the remote Git tree recursively for the target tag via `read_url_content`:
   `GET https://api.github.com/repos/{owner}/{repo}/git/trees/{tag}?recursive=1`
2. Build the **upstream path set**: collect all `tree[]` items with `type: "blob"` into a set of paths for cross-referencing.
3. Iterate through the upstream path set to classify each remote file:
   - **Check Sanctuary Denylist:** If item path matches any sanctuary pattern, mark as `🛡️ Preserved (Sanctuary)` and skip any download.
   - **Check Allowlist:** If item path does NOT match the Allowlist, skip item.
   - **Evaluate Local Existence:** Check if target path exists locally via `view_file`:
     - If file does not exist locally → Mark as `🟢 Added`.
     - If file exists locally → Mark as `🟡 Modified` for update.
4. **Deletion scan — identify `🔴 Removed` files:**
   Walk every local path in the Updatable Allowlist and legacy framework directories to find files that exist locally but are absent from the upstream release:
   - **For directory-glob allowlist entries** (`.agents/agents/**`, `.agents/skills/**`, `.agents/context/templates/**`): use `find_by_name` on each directory root to list all local files recursively.
   - **For single-file allowlist entries** (`.agents/rules/fact-checking.md`, `AGENTS.md`, `.agents/skills.json`, `framework.json`): check each individually using `view_file`; if the file exists locally, add it to the local file set.
   - **Legacy rule cleanup scan (`.agents/rules/**`):** to eliminate blind spots from historical framework versions (where templates and context resided under `rules/`), perform a recursive `find_by_name` on `.agents/rules/`. Any local file found here (e.g., `.agents/rules/references/**`, `.agents/rules/scoring.md`, `.agents/rules/output-formatting.md`) is evaluated for removal.
   For each local file found in the above scans:
   - **Retain valid upstream files:** If the file is `.agents/rules/fact-checking.md` and it is present in the upstream path set, keep it (do NOT mark as removed).
   - **Apply Precedence Rule:** `.agents/context/templates/**` is in the Allowlist (and therefore eligible for deletion); the broader `.agents/context/**` sanctuary does NOT apply to files under `templates/`.
   - **Skip if it matches the Sanctuary Denylist** (after applying the Precedence Rule above — zero-mutation guarantee for truly sanctuarized files).
   - **Skip if it is present in the upstream path set** (already classified in step 3 — it is Added or Modified, not Removed).
   - Otherwise → Mark as `🔴 Removed` (file exists locally but has been deleted, moved, or deprecated in the upstream release).
5. Consolidate delta metrics (count of files added, modified, removed, and preserved).


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
   | `🟢 Added` | `.agents/agents/sales-lead.md` | Core Orchestrator |
   | `🟡 Modified` | `.agents/context/scoring.md` | Core Rubric Update |
   | `🔴 Removed` | `.agents/rules/old-template.md` | Deleted upstream — will be removed locally |
   | `🛡️ Preserved` | `.agents/context/product-context.md` | Sanctuary (Company DNA) |
   | `🛡️ Preserved` | `.agents/context/customer-context.md` | Sanctuary (Target ICP) |
   | `🛡️ Preserved` | `reports/**` | Sanctuary (Generated Reports) |
4. **Mandatory Overwrite Warning:**
   > [!WARNING]
   > Any manual edits made directly to internal skills or HTML templates outside the protected context rules (`product-context.md`, `customer-context.md`) will be overwritten by upstream release defaults. Files marked `🔴 Removed` will be **permanently deleted** from your local workspace.
5. **Confirmation Gate:**
   - Explicitly request user approval in chat (e.g., *"Please confirm to proceed with the update: [confirm / cancel]"*).
   - **HALT execution** and wait for the user's explicit affirmation before performing Phase 4.

### Phase 4: Declarative Execution
Upon receiving explicit user confirmation:
1. For each file marked `🟢 Added` or `🟡 Modified`:
   - Download raw content via `read_url_content` from:
     `https://raw.githubusercontent.com/{owner}/{repo}/{tag}/{path}`
   - Write content to target file path using `write_to_file` (with `Overwrite: true`).
2. For each file marked `🔴 Removed`:
   - **Safety re-check:** confirm the file path does NOT match the Sanctuary Denylist (applying the Precedence Rule: `.agents/context/templates/**` is NOT sanctuary) before proceeding.
   - Derive the absolute workspace root from the path of `framework.json` read in Phase 1 (e.g., if `framework.json` is at `/Users/name/project/framework.json`, the workspace root is `/Users/name/project`).
   - Delete the local file using `run_command`: `rm "{absolute_workspace_root}/{path}"`
   - If the containing directory is now empty, remove it with `run_command`: `rmdir "{absolute_workspace_root}/{dir}"` (non-recursive — fail silently if non-empty).
3. Update `framework.json` at root:
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
| **Files Removed** | **{count_removed}** | Deleted locally — no longer in upstream |
| **Sanctuary Files Preserved** | **{count_preserved}** | Protected against overwrite |
| **Framework Version** | `v{new_version}` | Synced with upstream |

- **UI Refresh Recommendation (Conditional):**
  - Check whether any HTML templates under `.agents/context/templates/` or skill-specific `references/` (e.g., `index-template.html`, `context-template.html`, `radar-template.html`, `pipeline-summary-template.html`) were in the list of `🟢 Added` or `🟡 Modified` files during the update.
  - **If at least one template was updated:** append the following native Markdown callout directly below the Executive Briefing Card:
    > [!TIP]
    > Global UI templates were updated. Run `report` to refresh your portal, Company DNA, and pipeline views with the latest layout.
  - **If no templates were updated:** omit this callout entirely.
