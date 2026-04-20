---
description: List and filter tasks from the task tracker
argument-hint: "[--type <name>] [--status todo|in-progress|blocked|done]"
---

You are running the `/tasks` command. Read-only — no file writes, no git operations.

## Execution logic

1. **Parse arguments from `$ARGUMENTS`:**
   - `--type <name>` — filter by type of work (optional)
   - `--status <value>` — filter by status: `todo`, `in-progress`, `blocked`, `done` (optional)
   - No args = show all non-done tasks

2. **Read all files** in `tasks/` recursively that match `TASK-*.md` (across all type subdirectories).

3. **Parse frontmatter** from each file: id, title, type, status, priority, due, completed.

4. **Apply filters** from the parsed arguments.

5. **Sort:** by status (blocked → in-progress → todo → done), then priority (high → medium → low), then due date ascending.

6. **Print a markdown table:**

   | ID | Title | Type | Status | Priority | Due |
   |----|-------|------|--------|----------|-----|
   | TASK-001 | ... | ... | ... | ... | ... |

   If no tasks match the filter, say so clearly.

## ARGUMENTS: $ARGUMENTS
