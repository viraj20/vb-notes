---
description: Show today's task snapshot — overdue, due today, in progress, suggested focus
---

You are running the `/today` command. Read-only — no file writes, no git operations.

## Execution logic

1. **Read all files** in `tasks/` that match `TASK-*.md`.

2. **Parse frontmatter** from each: id, title, project, status, priority, due, completed.

3. **Print four sections:**

### 🔴 Overdue
Tasks where `due < today` AND `status != done`. Sort by due date ascending (oldest first).

### 📅 Due Today
Tasks where `due = today` AND `status != done`. Sort by priority.

### 🔄 In Progress
Tasks where `status = in-progress`. **Include tasks with no due date.** Sort by priority.

### 🎯 Suggested Focus (top 3)
Pick the 3 highest-priority items to work on today using this order:
1. Overdue tasks (oldest first)
2. Due-today tasks (high priority first)
3. In-progress tasks (high priority first)

4. If all sections are empty, say "All clear — no pending tasks for today."
