---
description: Mark a task as completed
argument-hint: "<TASK-ID>  e.g. TASK-001"
---

You are running the `/done` command. Read `CLAUDE.md` at the vault root first (the Task system section).

## Execution logic

1. **Parse arguments from `$ARGUMENTS`:** extract the task id (e.g. `TASK-001`). Case-insensitive.

2. **Sync:** `git pull --rebase origin main`

3. **Find the task file:** glob `tasks/**/TASK-NNN-*.md` recursively across all project subdirectories where NNN matches the numeric part of the given id. If not found, tell the user and stop.

4. **Update frontmatter:**
   - Set `status: done`
   - Add `completed: YYYY-MM-DD` (today's date in ISO format)

5. **Log** to `wiki/log.md`:
   ```
   ## [YYYY-MM-DD HH:MM] done: TASK-NNN
   - Updated: tasks/<project>/TASK-NNN-<slug>.md → status: done
   ```

6. **Commit and push:**
   ```
   git add -A
   git commit -m "done: TASK-NNN"
   git push origin main
   ```

7. **Confirm** to the user: "Marked **TASK-NNN** as done."

## ARGUMENTS: $ARGUMENTS
