---
description: Create a new task in the task tracker
argument-hint: "<title> --project <name> [--priority high|medium|low] [--due YYYY-MM-DD]"
---

You are running the `/task` command. Read `CLAUDE.md` at the vault root first (the Task system section).

## Execution logic

1. **Parse arguments from `$ARGUMENTS`:**
   - First unquoted or quoted string = task title
   - `--project <name>` — required; the project label (e.g. work, personal, finances, learning)
   - `--priority high|medium|low` — optional, default `medium`
   - `--due YYYY-MM-DD` — optional

2. **Sync:** `git pull --rebase origin main`

3. **Find next id:**
   - Glob `tasks/**/*.md` recursively across all project subdirectories
   - Extract the NNN from each filename, take the max, add 1
   - If no files exist, start at TASK-001

4. **Slugify the title:** lowercase, spaces → hyphens, strip characters that aren't alphanumeric or hyphens.

5. **Write `tasks/<project>/TASK-NNN-<slug>.md`** (create the project subfolder if it doesn't exist):
   ```yaml
   ---
   id: TASK-NNN
   title: <title>
   project: <project>
   status: todo
   priority: <priority>
   created: YYYY-MM-DD
   due: YYYY-MM-DD       # omit line if not provided
   tags: []
   ---
   ```
   Leave the body blank below the frontmatter.

6. **Log** to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD HH:MM] task: TASK-NNN <title>
   - Created: tasks/<project>/TASK-NNN-<slug>.md
   ```

7. **Commit and push:**
   ```
   git add -A
   git commit -m "task: TASK-NNN <title>"
   git push origin main
   ```

8. **Confirm** to the user: "Created **TASK-NNN** — <title> (`tasks/<project>/TASK-NNN-<slug>.md`)"

## ARGUMENTS: $ARGUMENTS
