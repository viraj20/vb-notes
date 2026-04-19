---
description: Health-check the wiki — broken links, orphans, stale drafts, contradictions, synthesis candidates
argument-hint: "[--fix-auto]"
---

You are running the `/lint-wiki` command. Read `CLAUDE.md` at the vault root first.

## Checks to run

### 1. Broken `[[wikilinks]]`
For every wiki page, resolve each `[[link]]`. If the target doesn't exist, list it.

### 2. Orphan pages
Pages with zero inbound links and `type != moc`. These are disconnected from the knowledge graph.

### 3. Frontmatter violations
Pages missing required fields per `CLAUDE.md`: `type`, `domain`, `status`, `created`, `updated`, `sources`.

### 4. Stale idea drafts
Pages in `wiki/ideas/` with `status: draft`, `created:` more than 30 days ago, and zero outbound or inbound links added since creation → propose `status: archived` or promotion.

### 5. Domain leakage → synthesis candidates
Pages whose inbound links come primarily (>60%) from a different domain. These may belong in `wiki/synthesis/`.

### 6. Uncited sources
Source files (`sources/**/*.md`) with `wiki_compiled: true` but no wiki page references them in `sources:` frontmatter.

### 7. Pending ingest queue depth
Count of sources with `wiki_compiled: false` or missing field. If >20, nudge user to run `/ingest-url`.

### 8. Trash expiry
Items in `.trash/` older than 30 days. Propose permanent delete (user must confirm).

### 9. Syncthing conflicts
Files matching `*.sync-conflict-*`. List for user resolution.

### 10. Ambiguous classifications
Files tagged `review: domain-uncertain` or `review: routing-needed`. List for user decision.

---

## Output

Write report to `output/lint-<YYYY-MM-DD>.md`:

```markdown
# Wiki lint report — <YYYY-MM-DD>

## Summary
- Total wiki pages: N
- Total source files: M (pending: X)
- Health score: A/B (B = total checks, A = checks passed)

## 1. Broken wikilinks (<count>)
...

## 2. Orphan pages (<count>)
...

(etc. per check)

## Actions offered
- `[a]` Archive stale idea drafts  (<N items>)
- `[p]` Permanently delete .trash/ items older than 30 days (<N items>)
- `[s]` Promote to synthesis (<N candidates>)
- `[r]` Review ambiguous classifications (<N items>)
```

---

## `--fix-auto` behavior

If passed, automatically apply **low-risk** fixes only:
- Add missing frontmatter fields with sensible defaults (keep `status: draft`).
- Fix kebab-case filename violations.
- Resolve `[[link]]` targets that differ only in case.

**Do not** auto-delete, auto-archive, or auto-promote — those need user confirmation.

Append operation to `wiki/log.md`:
```markdown
## [<YYYY-MM-DD HH:MM>] lint-wiki
- Health: A/B
- Auto-fixed: <summary> (if --fix-auto)
- Report: output/lint-<YYYY-MM-DD>.md
```
