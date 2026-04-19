---
type: moc
domain: synthesis
status: live
created: 2026-04-18
updated: 2026-04-18
sources: []
---

# Wiki index

The master catalog for VB's LLM wiki. Start here. Six domains, plus a synthesis layer for cross-domain pages.

## Domains

- [[work/index|Work — BookMyShow, SRE, systems]]
- [[finances/index|Finances — personal money, investing, India-specific]]
- [[learning/index|Learning — books, articles, podcasts, videos]]
- [[entertainment/index|Entertainment — movies, trips, photography]]
- [[ideas/index|Ideas — raw brainstorms awaiting crystallization]]
- [[synthesis/index|Synthesis — cross-domain pages bridging 2+ domains]]

## Recent activity

```dataview
TABLE file.mtime AS "Updated"
FROM "wiki"
WHERE type != "moc"
SORT file.mtime DESC
LIMIT 10
```

## How this wiki works

- **sources/** holds raw, immutable input (articles, highlights, transcripts).
- **inbox/** holds fleeting captures waiting for classification.
- **wiki/** (this folder) holds atomic, interlinked knowledge pages — maintained by Claude.
- See `CLAUDE.md` at the vault root for the full schema.
- See `wiki/log.md` for the chronological operation log.

## Quick operations

- `/ingest-url <url>` — pull an article into the wiki
- `/process-inbox` — classify everything in inbox/
- `/query "<question>"` — ask the wiki; cited answers
- `/lint-wiki` — health check
