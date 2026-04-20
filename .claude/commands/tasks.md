---
description: List and filter tasks from the task tracker
argument-hint: "[--project <name>] [--status todo|in-progress|blocked|done]"
---

You are running the `/tasks` command. Read-only — no file writes, no git operations.

## Execution logic

1. **Parse arguments from `$ARGUMENTS`:**
   - `--project <name>` — filter by project (optional)
   - `--status <value>` — filter by status: `todo`, `in-progress`, `blocked`, `done` (optional)
   - No args = show all non-done tasks

2. **Read all files** in `tasks/` recursively that match `TASK-*.md` (across all project subdirectories).

3. **Parse frontmatter** from each file: id, title, project, status, priority, due, completed.

4. **Apply filters** from the parsed arguments.

5. **Sort:** by status (blocked → in-progress → todo → done), then priority (high → medium → low), then due date ascending.

6. **Print a markdown table:**

   | ID | Title | Project | Status | Priority | Due |
   |----|-------|---------|--------|----------|-----|
   | TASK-001 | ... | ... | ... | ... | ... |

   If no tasks match the filter, say so clearly.

## ARGUMENTS: $ARGUMENTS
