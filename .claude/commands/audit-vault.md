---
description: One-time migration triage — classify every existing note, propose keep/archive/trash/review
argument-hint: "[--execute]"
---

You are running the `/audit-vault` command. This is the **one-time migration triage** that runs BEFORE any PARA-to-LLM-wiki restructure. Read `CLAUDE.md` at the vault root first.

**Two-phase execution: report first, then execute only with `--execute` flag after user approves.**

---

## Phase 1: Inventory and classification (no arg / default)

### Step 1: Walk all notes
Enumerate every `.md` file in the vault **except**:
- `.claude/`, `.obsidian/`, `.trash/`, `output/`, `wiki/`
- `CLAUDE.md`, files in `templates/`

For each note, collect: path, size, last-modified date, first 200 chars of content.

### Step 2: Apply safety rules (hard defaults, cannot be overridden at folder-level)

- `Journal/Daily Journal/*` → **keep & migrate** to `journal/daily/` (never archive, never trash)
- `Journal/Weekly Journal/*` → **keep & migrate** to `journal/weekly/`
- `3. Resources/Book Notes/Kindle Highlights/*` → **keep & migrate** to `sources/learning/books/`
- `Assets/*` → **keep & migrate** to `assets/`
- Notes modified within the last 180 days → default **keep** (user can override per-note)

### Step 3: Classify each remaining note

Propose one of:
- **keep & migrate** with a target path from the Migration Map (see plan file)
- **archive** → `archive/<original-folder-name>/` (preserves context)
- **trash** → `.trash/` (reversible 30 days)
- **review** → `inbox/review/` (deferred)

Signals favoring **trash**:
- Filename matches `Untitled*.md`
- Content <50 chars or obviously placeholder
- Duplicate of another note (same content hash)
- No modification in >2 years AND <200 chars

Signals favoring **archive**:
- Not modified in >1 year
- Historically relevant but no active links
- Content reads as a completed thought, not an active project

Signals favoring **review**:
- Content unclear about topic
- Filename doesn't match content
- Multiple domains overlap ambiguously

### Step 4: Write report to `output/vault-audit-<YYYY-MM-DD>.md`

Format:

```markdown
# Vault audit — <YYYY-MM-DD>

## Summary
- Total notes: <N>
- Proposed actions:
  - keep & migrate: <N>
  - archive: <N>
  - trash: <N>
  - review: <N>
- Protected by safety rules: <N>

## Folder-level bulk proposals (user approves in one pass)

### 1. Projects/ (<N notes>)
- <X> → keep & migrate to wiki/work/projects/
- <Y> → archive (last modified >1 year)
- <Z> → review

### 2. Areas/Habits/ (<N>)
- All → keep & migrate to trackers/habits/

### 3. Resources/Book Notes/Kindle Highlights/ (<N>)
- All → keep & migrate to sources/learning/books/ (protected)

(etc. per folder)

### Root-level loose notes (<N>)
Individual review needed — see Flagged table below.

## Flagged items for per-note review

| # | Path | Last modified | Size | Preview | Proposed | Reason |
|---|---|---|---|---|---|---|
| 1 | Entrepreneurship masterclass Ali Abdaal.md | 2024-05-06 | 527B | "… first 80 chars …" | keep → wiki/ideas/ | root loose |
| 2 | Untitled.md | 2024-01-12 | 0B | (empty) | trash | empty file |
| … | | | | | | |

## Next steps for user

1. Review this report.
2. For folder-level proposals — approve, modify, or reject each block.
3. For flagged items — walk the table, approve/override each row.
4. Once decisions are final, run `/audit-vault --execute` to apply.
```

### Step 5: Stop. Wait for user.

Do not move any files. This phase is decision-only.

---

## Phase 2: Execute (`--execute` arg)

1. **Re-read** the approved `output/vault-audit-<YYYY-MM-DD>.md`.
2. **Verify Obsidian is configured** for auto-link-update. Prompt user to confirm: "Settings → Files & Links → Automatically update internal links: ON?"
3. **Create** new top-level dirs: `sources/`, `inbox/`, `inbox/review/`, `journal/`, `trackers/`, `archive/`. (Wiki and `.claude`, `output` already exist.)
4. **Execute moves** per the approved audit, in this order for maximum link-update coherence:
   - Folder-level migrations first (bulk `mv`)
   - Per-note migrations second
   - Archives third
   - Trash moves last
5. **Write migration log** to `output/migration-log-<YYYY-MM-DD>.md`:
   ```markdown
   # Migration log — <YYYY-MM-DD>
   
   ## Migrated (<N>)
   - <old path> → <new path>
   ...
   
   ## Archived (<N>)
   - <old path> → archive/<new path>
   ...
   
   ## Trashed (<N>) — recoverable until <YYYY-MM-DD + 30 days>
   - <old path> → .trash/<new path>
   ...
   
   ## Deferred to inbox/review/ (<N>)
   - <path>
   ...
   ```
6. **Append to `wiki/log.md`:**
   ```markdown
   ## [<YYYY-MM-DD HH:MM>] migration — bootstrap
   - Migrated <N> notes per output/vault-audit-<YYYY-MM-DD>.md
   - Full log: output/migration-log-<YYYY-MM-DD>.md
   ```

---

## Guardrails

- **Never execute without `--execute` flag.** Phase 1 is strict read-only-plus-report.
- **Never trash a journal entry or Kindle highlight** regardless of user input — protected categories.
- **Never delete a file** — "trash" always means move to `.trash/`.
- If Obsidian auto-link-update is not enabled, STOP and tell the user to enable it first (prevents link breakage on rename).
- After execution, prompt user to spot-check 10 random notes in Obsidian to confirm links resolved.
