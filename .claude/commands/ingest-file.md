---
description: Ingest a local file (PDF, markdown, Kindle export, transcript) into the wiki
argument-hint: "<path-to-file> [--domain=<domain>]"
---

You are running the `/ingest-file` command. Read `CLAUDE.md` at the vault root first.

## Execution logic

1. **Read the file** at `<path>`. Supports markdown, PDF (via extraction), plain text, Kindle `.md` exports, meeting-transcript format.
2. **Determine the domain:**
   - If `--domain=<name>` is passed, use it.
   - Otherwise apply **source-format defaults** (Kindle → learning/books, meeting transcripts → work/meetings, etc.).
   - Otherwise fall back to content-based classification per `CLAUDE.md`.
3. **If the file is not already in `sources/<domain>/`:** move it there with filename `<YYYY-MM-DD>-<slug>.md` (preserving original extension if PDF), and add source frontmatter:
   ```yaml
   ---
   author: <if known>
   captured: <today>
   captured_via: ingest-file
   original_path: <original path>
   wiki_compiled: false
   ---
   ```
4. **Compile into wiki** per the same rules as `/ingest-url` — 3–8 wiki pages touched, cross-linked, synthesis detected, MOC updated, log appended.

## Guardrails

- Do not delete the original file — move, don't copy+delete, unless user passes `--copy` (then preserve original).
- For large files (>50KB), offer to summarize in chunks rather than loading entire content into context.
- Never compile a file that already has `wiki_compiled: true` without `--force`.
