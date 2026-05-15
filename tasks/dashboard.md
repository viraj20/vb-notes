---
type: dashboard
updated: 2026-04-20
---

# Task Dashboard

> Use `/task`, `/done`, `/tasks`, `/today` to manage tasks via Claude.

---

## 🔴 Overdue

```dataview
TABLE title, type, priority, due
FROM "tasks"
WHERE status != "done" AND due < date(today)
SORT priority ASC, due ASC
```

---

## 📅 Due Today

```dataview
TABLE title, type, priority
FROM "tasks"
WHERE status != "done" AND due = date(today)
SORT priority ASC
```

---

## 🔄 In Progress

```dataview
TABLE title, type, priority, due
FROM "tasks"
WHERE status = "in-progress"
SORT priority ASC, due ASC
```

---

## 📋 Backlog

```dataview
TABLE title, priority, due
FROM "tasks"
WHERE status = "todo"
GROUP BY type
SORT priority ASC, due ASC
```

---

## ✅ Completed This Week

```dataview
TABLE title, type, completed
FROM "tasks"
WHERE status = "done" AND completed >= date(today) - dur(7 days)
SORT completed DESC
```
