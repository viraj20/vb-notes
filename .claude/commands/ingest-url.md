---
description: Ingest a URL (or process the pending queue) into the wiki
argument-hint: "[url | --force <path> | (no args = process queue)]"
---

You are running the `/ingest-url` command for VB's LLM wiki. Read `CLAUDE.md` at the vault root first to understand the schema.

## Execution logic

### If invoked with a URL argument: `/ingest-url <url>`

1. Apply the **URL routing rules** from `CLAUDE.md` to pick `<domain>`.
2. Fetch the URL (use WebFetch or equivalent).
3. Save full article markdown to `sources/<domain>/<YYYY-MM-DD>-<slug>.md` with frontmatter:
   ```yaml
   ---
   url: <original URL>
   author: <extracted if available>
   captured: <today YYYY-MM-DD>
   captured_via: ingest-url
   wiki_compiled: false
   ---
   ```
4. Then proceed to **Compile step** below.

### If invoked with `--force <source-path>`

Re-compile an already-ingested source. Skip fetch, go straight to Compile.

### If invoked with no arguments

Process the pending queue, **max 10 items per run** for reviewability:

1. Read `inbox/urls.md` line-by-line. Each non-blank, non-comment line is a URL.
2. Scan `sources/**/*.md` for files where frontmatter has `wiki_compiled: false` or is missing the field entirely.
3. For each pending item:
   - URL queue entry → fetch, save to `sources/`, compile, remove line from `inbox/urls.md` on success.
   - Source file → compile, flip `wiki_compiled: true`.
4. Stop after 10 items. Surface how many remain pending.
5. If any fetch fails, leave the URL in the queue with a `# FAILED <YYYY-MM-DD>: <reason>` comment above it.

---

## Compile step (the core work)

For the source being ingested:

1. **Read the source** end to end. Identify 3–8 load-bearing concepts, entities, or insights worth a wiki page.
2. **Check each** against existing `wiki/<domain>/` pages. If a page exists, update it (add insights, cross-links, new "source" entry). If not, create it.
   **Coverage rule for Kindle highlight sources.** The compiled book page must cite at least `ceil(0.6 × N)` distinct highlights, where N is the source's highlight count. "Cite" = a direct quote followed by `loc X` citation or an explicit `(loc X)` parenthetical. Load-bearing highlights (3–8) drive the main sections; the remaining highlights required to hit 60% live in an **"Other notable passages"** section as 3–6 thematic paragraphs, each with a one-sentence interpretive frame and 2–5 grouped `loc X` citations. Never build a raw-highlights appendix.
   **Placeholder exemption.** Sources with fewer than 5 highlights are exempt from the 60% rule — keep the page brief; sparse material is the signal.
3. **Frontmatter** for every new wiki page:
   ```yaml
   ---
   type: concept | entity | source-summary | synthesis | moc
   domain: <one of six>
   status: draft
   created: <today>
   updated: <today>
   sources: [<path to source file>]
   ---
   ```
4. **Cross-link aggressively but within budget** — each page gets max 15 outgoing `[[wikilinks]]`. Link to adjacent concepts, entities, MOCs.
5. **Synthesis detection** — if the source's concepts bridge two or more domains (e.g., an SRE article with finance implications), create a synthesis page in `wiki/synthesis/` that links to both domain pages.
6. **Update domain MOC** (`wiki/<domain>/index.md`) if a new major topic emerged.
7. **Append to `wiki/log.md`**:
   ```markdown
   ## [<YYYY-MM-DD HH:MM>] ingest-url <url-or-source-path>
   - Created: <list of new wiki paths>
   - Updated: <list of updated wiki paths>
   - Synthesis: <any new synthesis pages, or "none">
   - Source: <source file path>
   ```

---

## Guardrails

- Never modify files in `sources/`, `journal/`, `archive/`, `.trash/`.
- Never create a wiki page without at least one `[[wikilink]]` and one MOC reference.
- If the URL can't be classified (no rule matches, content too ambiguous): file under `sources/ideas/` with `wiki_compiled: false` and tag `review: routing-needed` — do NOT compile until user confirms.
- Stop at 10 items per run; print a summary like: `Ingested 10 items. 7 remaining pending.`
