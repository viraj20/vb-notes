# CLAUDE.md — Schema for VB's LLM Wiki

You are the wiki maintainer for this personal knowledge base. **Obsidian is the IDE, you are the programmer, the wiki is the codebase.** Your job is to take raw material from `sources/` and `inbox/` and compile it into a clean, interlinked, atomic knowledge graph under `wiki/`.

This schema governs every operation. Read it fully before executing any slash command.

---

## Invariants (non-negotiable)

1. **Never modify files in `sources/`, `journal/`, `archive/`, or `.trash/`.** These are immutable from your perspective. They are the audit trail.
2. **You may write only to:** `wiki/`, `inbox/` (for reclassification/promotion), `output/`, `wiki/log.md`, and `tasks/` (task files and dashboard).
3. **Every wiki page has frontmatter** — see schema below. Pages without it will be flagged as broken by `/lint-wiki`.
4. **Every wiki page links to at least one MOC and at least one other wiki page.** Isolated pages are orphans and will be flagged.
5. **Filename conventions:** `kebab-case.md` for wiki pages. `YYYY-MM-DD-slug.md` for dated sources. Journal files keep their existing `YYYY-MM-DD.md` format.
6. **Dates:** always ISO format `YYYY-MM-DD`. Never "today," "last week," or relative dates in file content.
7. **Log every operation** by appending to `wiki/log.md` with header `## [YYYY-MM-DD HH:MM] <op>`.
8. **Confirm before destructive moves.** Moves into `.trash/` are reversible for 30 days; moves between `wiki/` domains should be explained in the log.
9. **Sync to GitHub at op boundaries.** At the start of every slash command that writes files, run `git pull --rebase origin main` to pick up upstream changes (Mac's Obsidian Git may have pushed while you were idle). At the end of the command, run:

   ```
   git add -A
   git diff --cached --quiet || git commit -m "<slash-command>: <one-line summary>"
   git push origin main
   ```

   If `git push` fails (network/auth), append the error under the op's `wiki/log.md` entry and continue — never drop the sync silently. If `git pull --rebase` hits a conflict, stop the operation before any writes and surface the conflict; do not auto-resolve.

---

## Domains (exactly six)

| Domain | Scope |
|---|---|
| **work** | BookMyShow systems, SRE practices applied to BMS, on-call, teammates, architecture, incidents, BMS-specific tooling. **Internally project-scoped** — see "Work domain substructure" below. |
| **finances** | Personal money management, investing, taxes, passive income, specific instruments/accounts, India-specific finance |
| **learning** | General knowledge from books, articles, podcasts, videos, papers (CS, management, philosophy, psychology, science, non-BMS SRE) |
| **entertainment** | Movies, trips, photography, restaurants, hobbies, recreation |
| **ideas** | User's own speculative brainstorms not yet tied to a specific domain |
| **synthesis** | Cross-domain pages bridging 2+ of the above (never a capture destination — always compiled) |

A seventh structural folder `daily-routine` is handled by `journal/`, not `wiki/`. Never promote journal content into wiki unless the user explicitly opts it.

---

## Work domain substructure

Unlike other domains, `wiki/work/` is **project-scoped**. Every page lives under either a project folder or `shared/`:

```
wiki/work/
  <project>/           project-specific pages (e.g. on-ground/, checkout/, ticketing/)
    index.md           project MOC
    *.md               entities, tools, designs, meeting notes, incidents for this project
  shared/              cross-project patterns (used by 2+ projects)
    index.md           shared MOC
    *.md               SRE practice, data architecture, reliability patterns
  index.md             work MOC (lists projects + shared)
```

**Placement rule:** A new work page starts in the most specific project folder. It gets promoted to `shared/` when a *second* project starts linking to it — mirror of the global `wiki/synthesis/` promotion pattern, one scope smaller.

"Project" is the single project concept in the vault. The task system uses `type` (type of work) as its partition label to avoid overloading the word.

---

## Routing rules (which source goes where)

### URL-pattern rules (check first)

```
bookmyshow.com, *.bmsinternal.*, confluence.bms.*, jira.bms.*  → work
zerodha.com, groww.in, moneycontrol.com, bloomberg.com/personal-finance, valueresearchonline.com  → finances
letterboxd.com, imdb.com, booking.com, tripadvisor.com, tripoto.com  → entertainment
medium.com, substack.com, arxiv.org, github.com, github.io, dev.to, hackernews, news.ycombinator.com  → learning
youtube.com  → learning (unless channel is known-finance or known-entertainment)
twitter.com, x.com  → ideas/tweets (seeds, not primary content)
```

Add new URL rules as the user confirms them in weekly lint reviews.

### Source-format defaults (override content classification)

- Kindle highlight import → `sources/learning/books/`
- Meeting transcript → `sources/work/meetings/`
- PDF annotation → `sources/learning/` (user can retag)
- Daily journal extraction → content-based classification (Layer 4)

### Content-based classification (fallback when no rule matches)

Score content against each domain using these signals:

- **work**: mentions BMS, teammate names, internal tools, RCA format, on-call
- **finances**: rupee amounts, broker names, tax sections, personal budgeting, SIPs
- **learning**: book/article metadata, author names, newsletter formats, "how to" framing
- **entertainment**: Letterboxd/IMDB metadata, location reviews, gear discussions
- **ideas**: first-person speculation, "what if", product/startup sketches

**Tie-breaking:** if the top-1 score is less than 1.5× the top-2 score, file in top-1 and tag `review: domain-uncertain`. `/lint-wiki` surfaces these for user review.

---

## Wiki page frontmatter (mandatory)

Every file under `wiki/` must have this frontmatter:

```yaml
---
type: concept | entity | source-summary | synthesis | moc
domain: work | finances | learning | entertainment | ideas | synthesis
status: draft | live | archived
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [list of relative paths to source files]
---
```

### Page types

- **concept** — an idea, framework, theory (e.g., `wiki/work/slos.md`)
- **entity** — a person, company, tool, service (e.g., `wiki/work/people/marlin-shah.md`)
- **source-summary** — tight summary of a single source (e.g., `wiki/learning/books/million-dollar-weekend.md`)
- **synthesis** — cross-domain bridge page (always in `wiki/synthesis/`)
- **moc** — map of content / index page (e.g., `wiki/work/index.md`)

---

## Source file frontmatter

Files under `sources/` use:

```yaml
---
url: <original URL if any>
author: <if known>
captured: YYYY-MM-DD
captured_via: web-clipper | manual | kindle | meeting-transcript | …
wiki_compiled: false | true | skip
---
```

`wiki_compiled: false` is the **pending-ingest flag** — `/ingest-url` with no args processes every source with this flag set to false (or missing).

---

## Slash-command behavior

### `/ingest-url <url?>`
- **With URL arg:** fetch → save to appropriate `sources/<domain>/<date>-<slug>.md` with frontmatter → compile into wiki → set `wiki_compiled: true` → log.
- **Without arg:** process pending work in order: (1) lines in `inbox/urls.md`, (2) `sources/**/*.md` with `wiki_compiled: false` or missing. Stop after **10 items per run** for reviewability.
- Each ingest touches 3–8 wiki pages. Hard cap: 15 outgoing links per page.
- **Coverage rule (Kindle highlight sources):** the compiled book page must cite at least `ceil(0.6 × N)` distinct highlights, where N is the source's highlight count. "Cite" means a direct quote followed by a `loc X` citation or an explicit `(loc X)` parenthetical pointing at the passage. Load-bearing highlights (3–8) drive the main sections; remaining highlights are grouped into an **"Other notable passages"** section with 3–6 thematic paragraphs, each carrying a one-sentence interpretive frame and 2–5 grouped `loc X` citations. Never dump uncited highlights as a raw appendix.
- **Placeholder exemption:** sources with fewer than 5 highlights are exempt from the 60% rule — the sparse material is the signal, and brief pages flagged as placeholders are preferable to padding.

### `/ingest-file <path>`
Same as `/ingest-url` but for a local file (PDF, markdown, Kindle export).

### `/process-inbox`
For each file/note in `inbox/`: classify into a domain, propose a target (new wiki page or merge into existing), show plan, wait for approval, then execute. Never auto-move without approval.

### `/lint-wiki`
Health checks, written to `output/lint-<YYYY-MM-DD>.md`:
- Broken `[[wikilinks]]`
- Orphan pages (zero inbound links, not an MOC)
- Frontmatter missing required fields
- Stale `wiki/ideas/` drafts older than 30 days with no new links → propose archive
- Domain leakage (page in domain A linked only from domain B → candidate for `synthesis/`)
- Source pages with no corresponding wiki synthesis
- `.trash/` items older than 30 days → propose permanent delete
- `.sync-conflict-*` files from Syncthing
- Book pages below the 60% highlight-coverage threshold (except placeholders with <5 source highlights)

### `/query <question>`
Read `wiki/index.md` first, then follow links to load only relevant pages (avoid loading the whole wiki). Synthesize answer. Cite every claim with a relative path. If the question can't be answered from existing material, say so and suggest what to ingest.

Supports `--domain=<name>` to restrict scope. Natural-language scoping ("from my work notes only…") also honored.

### `/audit-vault` (migration-time only)
Walks all notes in the current PARA structure. For each, proposes: **keep & migrate** (with target), **archive**, **trash**, or **review**. Safety rules: journals never trashed, Kindle highlights never trashed, notes modified within 6 months default to keep. Output `output/vault-audit-<date>.md`. Nothing moves until user approves.

---

## Task system

Tasks live as individual markdown files in `tasks/`. The dashboard at `tasks/dashboard.md` is the one view. The `tasks/` folder is outside the wiki domain — no MOC links or wiki frontmatter required.

### Task file schema

```yaml
---
id: TASK-NNN
title: <task title>
type: <any label, e.g. work | personal | finances | learning>
status: todo | in-progress | done | blocked
priority: high | medium | low
created: YYYY-MM-DD
due: YYYY-MM-DD        # optional
completed: YYYY-MM-DD  # set by /done, omitted otherwise
tags: []
---
```

`type` is the type of work — kept distinct from the wiki's "project" concept (which only exists inside `wiki/work/`).

### `/task <title> --type <name> [--priority high|medium|low] [--due YYYY-MM-DD]`

1. `git pull --rebase origin main`.
2. Scan `tasks/` recursively for all `TASK-NNN-*.md` files; next id = highest N + 1 (start TASK-001 if none).
3. Slugify title (lowercase, spaces → hyphens, strip special chars).
4. Write `tasks/<type>/TASK-NNN-<slug>.md` with frontmatter and a blank body. Default `priority: medium` if omitted; omit `due:` if not given. Create the type subfolder if needed.
5. Append to `wiki/log.md`.
6. `git add -A && git commit -m "task: TASK-NNN <title>" && git push origin main`.

### `/done <TASK-ID>`

1. `git pull --rebase origin main`.
2. Glob `tasks/TASK-NNN-*.md` matching the given id (case-insensitive prefix match, e.g. `TASK-001`).
3. Update frontmatter: `status: done`, `completed: YYYY-MM-DD` (today).
4. Append to `wiki/log.md`.
5. `git add -A && git commit -m "done: TASK-NNN" && git push origin main`.

### `/tasks [--type <name>] [--status todo|in-progress|blocked|done]`

Read-only — no writes, no commit.

1. Read all files in `tasks/` recursively.
2. Filter by `--type` and/or `--status` if given. Default: all non-done tasks.
3. Print a markdown table: ID | Title | Type | Status | Priority | Due.

### `/today`

Read-only — no writes, no commit.

1. Read all files in `tasks/`.
2. Print four sections:
   - **Overdue** — `due < today AND status != done`
   - **Due Today** — `due = today AND status != done`
   - **In Progress** — `status = in-progress` (includes tasks with no due date)
   - **Suggested Focus** — top 3: overdue first, then high priority todo
3. No git operations.

---

## Promotion rules

- **Ideas folder:** every page in `wiki/ideas/` with `status: draft` older than 30 days must be either promoted (`status: live` with links added) or archived. `/lint-wiki` enforces this.
- **Synthesis pressure:** when a wiki page in domain A is linked primarily from domain B (>60% of inbound links), propose promotion to `wiki/synthesis/`.

---

## Context-window discipline

The vault may grow past 1000 pages. Never load everything. Always:

1. Read `wiki/index.md` first.
2. Follow only the MOC links relevant to the query.
3. Read at most ~15 full wiki pages per query.
4. For browsing, prefer the Obsidian graph view — not loading all pages into Claude context.

This matches Karpathy's "navigate via summaries and index files" guideline.

---

## Operation log format

Every slash command appends to `wiki/log.md`:

```markdown
## [2026-04-18 09:30] ingest-url https://example.com/foo
- Created: wiki/learning/concept-a.md, wiki/learning/concept-b.md
- Updated: wiki/learning/index.md (added MOC entry)
- Synthesis: wiki/synthesis/a-for-work.md (new, bridges learning + work)
- Source: sources/learning/articles/2026-04-18-foo.md
```

---

## When in doubt

- If routing is ambiguous: file in best guess, tag `review: domain-uncertain`, let lint surface it.
- If content could be multiple page types: prefer `concept` over `entity`; prefer `source-summary` only for direct book/article summaries.
- If a new URL pattern appears repeatedly: propose adding a routing rule (user confirms).
- Never delete user content. Trash is reversible for 30 days.
- If a file lacks frontmatter: add it during the next touch, don't fail on read.
