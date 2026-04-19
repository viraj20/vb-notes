---
description: Ask a question of the wiki — grounded, cited answers from your own notes
argument-hint: "<question> [--domain=<name>] [--save]"
---

You are running the `/query` command. Read `CLAUDE.md` at the vault root first.

## Execution logic

1. **Parse arguments:**
   - `--domain=<name>` restricts search to `wiki/<name>/` + `sources/<name>/`.
   - Natural-language scoping ("from my work notes only…") also honored.
   - `--save` saves the answer to `output/query-<YYYY-MM-DD>-<slug>.md`.
2. **Load the index first** — read `wiki/index.md` to understand what's available.
3. **Identify relevant MOCs** — based on keywords in the question, follow 1–3 MOC links to get the relevant domain indexes.
4. **Load specific pages** — read the 5–15 most relevant wiki pages. Do NOT read everything.
5. **Check sources if needed** — if wiki pages cite a source that seems directly relevant, load the source for details.
6. **Synthesize** — compose an answer that:
   - Directly answers the question
   - Cites specific pages with relative paths, e.g., `wiki/work/slos.md` or `sources/learning/articles/2026-04-10-foo.md`
   - Uses `[[wikilinks]]` in the answer so Obsidian resolves them on display
   - Identifies gaps: if the question can't be fully answered, say what's missing and suggest what to ingest
7. **If `--save`:** write the answer to `output/query-<YYYY-MM-DD>-<slug>.md` with frontmatter:
   ```yaml
   ---
   question: <original question>
   domain_filter: <if any>
   asked: <YYYY-MM-DD HH:MM>
   pages_consulted: [list]
   ---
   ```
8. **Log** to `wiki/log.md`:
   ```markdown
   ## [<YYYY-MM-DD HH:MM>] query "<first 60 chars>…"
   - Pages consulted: <N>
   - Saved to: <output path if --save, else "not saved">
   ```

---

## Answer format

Every answer follows this shape:

```markdown
## Answer
<direct response, 2–6 paragraphs, cites inline>

## Evidence
- [[wiki/work/slos]] — "…specific claim…"
- [[sources/learning/articles/2026-04-10-foo]] — "…specific quote…"

## Gaps (if any)
<what you don't have enough material to answer, and what to ingest to close the gap>
```

---

## Guardrails

- **Never invent citations.** If you can't find a supporting page, say so.
- **Never load the whole wiki.** Max 15 full page reads per query.
- **Honor domain filters strictly.** If `--domain=finances`, do not quote from `wiki/work/` even if tangentially relevant — instead note the gap and suggest a synthesis query.
- **Cross-domain questions** should check `wiki/synthesis/` specifically.
