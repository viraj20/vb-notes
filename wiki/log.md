---
type: moc
domain: synthesis
status: live
created: 2026-04-18
updated: 2026-04-18
sources: []
---

# Operation log

## [2026-04-20 00:00] task: TASK-001 create a doc for on ground ops
- Created: tasks/TASK-001-create-a-doc-for-on-ground-ops.md

## [2026-04-20 12:30] refactor: work wiki → project-scoped + shared; task field project → type
- wiki/work/ restructured: tools/, concepts/, projects/ retired in favour of <project>/ + shared/
- Moved (git mv, history preserved):
  - wiki/work/tools/atomx.md → wiki/work/on-ground/atomx.md
  - wiki/work/projects/atomx-ontology-design.md → wiki/work/on-ground/atomx-ontology-design.md
  - wiki/work/concepts/{medallion-data-pipeline,data-ontology,canonical-enum-layer,graph-traversal-hop-depth}.md → wiki/work/shared/
- Wikilinks updated across all 6 pages
- New MOCs: wiki/work/on-ground/index.md, wiki/work/shared/index.md
- Updated: wiki/work/index.md (new project-scoped structure)
- CLAUDE.md: added "Work domain substructure" section
- Task system: frontmatter field `project` → `type`; `/task`, `/tasks` flag `--project` → `--type`
- Updated: tasks/dashboard.md (dataview queries), tasks/work/TASK-001-*.md (frontmatter), .claude/commands/{task,tasks,today,done}.md
- CLAUDE.md task schema updated

## [2026-04-20 12:00] ingest-file sources/work/projects/on-ground/research/atomx-research.md
- Source frontmatter added (wiki_compiled: true) to source file in place
- Created: wiki/work/tools/atomx.md (entity — BMS portfolio, closed-loop cashless POS)
- Created: wiki/work/concepts/medallion-data-pipeline.md (concept — bronze/silver/gold)
- Created: wiki/work/concepts/data-ontology.md (concept — Palantir-style object/link/action model)
- Created: wiki/work/concepts/canonical-enum-layer.md (concept — schema insulation pattern)
- Created: wiki/work/concepts/graph-traversal-hop-depth.md (concept — SQL vs graph DB, AND collapse)
- Created: wiki/work/projects/atomx-ontology-design.md (draft proposal — persistent medallion + ontology on Databricks)
- Updated: wiki/work/index.md (new Data architecture section; Tools and Projects populated)
- Domain: work (BMS portfolio company; internal tooling)

## [2026-04-19 00:00] query "can you share one quote from a book I have read"
- Pages consulted: 3 (wiki/index.md, wiki/learning/index.md, wiki/learning/books/siddhartha.md)
- Saved to: not saved

Append-only chronological record of every wiki operation. Newest at bottom. Format: `## [YYYY-MM-DD HH:MM] <op>` followed by a bulleted summary of what changed.

Use `/lint-wiki` to audit; use `/query` to ask questions; use `/ingest-url`, `/ingest-file`, `/process-inbox` to add material.

---

## [2026-04-18 init] bootstrap
- Vault restructured from PARA to Karpathy-style LLM wiki.
- Schema established at `CLAUDE.md`.
- Scaffolding: `.claude/commands/`, `output/`, `wiki/`.
- Slash commands created: `/ingest-url`, `/ingest-file`, `/process-inbox`, `/lint-wiki`, `/query`, `/audit-vault`.
- Pending: migration triage via `/audit-vault`, then execute with `--execute`.

## [2026-04-18 18:52] migration — bootstrap
- Simplified "park-and-triage" strategy: kept only Book Notes; archived everything else.
- Migrated 63 notes: `3. Resources/Book Notes/` → `sources/learning/books/` (preserves `Kindle Highlights/` and `My Notes/` subtrees).
- Archived 313 notes to `archive/` (preserving original folder structure: `1. Projects/`, `2. Areas/`, `3. Resources/`, `4. Archives/`, `Journal/`, `Meeting Notes/`, `Assets/`, `Ink/`, `Scratch Pad/`, plus 44 root-level loose notes to `archive/loose/`).
- **Safety-rule overrides (user-authorised):** `Journal/*` archived instead of going to protected `journal/`; `Assets/*` archived instead of going to protected `assets/`. Nothing deleted — all content recoverable via `mv` back from `archive/`.
- Trashed: 0. Deferred to `inbox/review/`: 0.
- Full plan: `output/vault-audit-2026-04-18.md`.
- Full log: `output/migration-log-2026-04-18.md`.

## [2026-04-19] scaffold + frontmatter backfill
- Backfilled source frontmatter (`captured`, `captured_via`, `wiki_compiled: false`) on all 63 notes in `sources/learning/books/`. 60 had existing frontmatter (Kindle's `kindle-sync` block, Sophie's World style) — appended to it; 3 had none — prepended fresh block.
- Scaffolded six domain MOCs: `wiki/work/index.md`, `wiki/finances/index.md`, `wiki/learning/index.md`, `wiki/entertainment/index.md`, `wiki/ideas/index.md`, `wiki/synthesis/index.md`. Each links back to `wiki/index.md` (satisfies invariant #4) and lists archive seed material for future ingestion.
- Wiki now ready for batched compilation. Run `/ingest-url` (no args) to process the next 10 unsynced sources.

## [2026-04-19 10:15] ingest-url (no args) — first compile batch
- Scope: 10 pending source files → 8 book source-summary pages (two pairs merged: Millionaire Fastlane = My Notes + DeMarco Kindle; Systems Performance = personal note + Gregg Kindle).
- Created book pages under `wiki/learning/books/`:
  - `site-reliability-engineering.md` (Murphy et al.)
  - `designing-data-intensive-applications.md` (Kleppmann)
  - `systems-performance.md` (Gregg) — merges 2 sources
  - `system-design-interview.md` (Xu)
  - `ikigai.md`
  - `sophies-world.md` (partial — pre-Socratics to Plato)
  - `the-millionaire-fastlane.md` (DeMarco) — merges 2 sources
  - `the-million-dollar-weekend.md`
- Created concept pages under `wiki/learning/concepts/`: `error-budget.md`, `toil.md`, `golden-signals.md`, `use-method.md`, `latency-vs-throughput.md`, `scalability.md`, `fault-vs-failure.md`, `flow-state.md`.
- Created concept pages under `wiki/finances/concepts/`: `wealth-trinity.md`, `cents-framework.md`, `wealth-equation.md`.
- Synthesis: `wiki/synthesis/sre-practice-for-bms.md` (new, bridges learning SRE canon → work/BMS application — will densify as work/ gains pages).
- Updated MOCs: `wiki/learning/index.md` (Concepts section + Books entries), `wiki/finances/index.md` (Concepts section), `wiki/synthesis/index.md` (Active synthesis pages entry).
- Flipped `wiki_compiled: true` on all 10 source files.
- Sources processed:
  - `sources/learning/books/My Notes/The million dollar weekend.md`
  - `sources/learning/books/My Notes/The Millionaire Fastlane.md`
  - `sources/learning/books/My Notes/Sophie's World.md`
  - `sources/learning/books/System Performance by Brendon Gregg.md`
  - `sources/learning/books/Ikigai.md`
  - `sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md`
  - `sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md`
  - `sources/learning/books/Kindle Highlights/Xu-System Design Interview – An insiders guide.md`
  - `sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md`
  - `sources/learning/books/Kindle Highlights/DeMarco-The Millionaire Fastlane.md`
- **Pending:** 53 remaining source files with `wiki_compiled: false` in `sources/learning/books/Kindle Highlights/`. Re-run `/ingest-url` for the next batch.
- **Known issue to resolve next pass:** `Gaarder-Sophies World.md` Kindle highlights still pending — should be merged into `wiki/learning/books/sophies-world.md` (currently only cites the personal note).
- **Review flag:** VB's "freedom number = 300000" in Million Dollar Weekend note is unit-ambiguous (/mo vs /yr). Flagged inside `wiki/learning/books/the-million-dollar-weekend.md`.

## [2026-04-19 11:30] ingest-url (no args) — second compile batch
- Scope: 10 pending source files → 9 new book source-summary pages + 1 updated (Sophie's World now merges both VB's note and Gaarder's Kindle highlights).
- Created book pages under `wiki/learning/books/`:
  - `mans-search-for-meaning.md` (Frankl)
  - `how-to-win-friends-and-influence-people.md` (Carnegie, placeholder — single highlight)
  - `start-with-why.md` (Sinek)
  - `leaders-eat-last.md` (Sinek, placeholder — single highlight)
  - `the-48-laws-of-power.md` (Greene)
  - `predictably-irrational.md` (Ariely)
  - `the-100-startup.md` (Guillebeau, placeholder)
  - `the-four-steps-to-the-epiphany.md` (Blank)
  - `the-gig-economy.md` (Mulcahy)
- Updated book page: `wiki/learning/books/sophies-world.md` (merged Gaarder Kindle highlights into existing page — full pre-Socratics → Athens arc now cited; resolves prior-batch flag).
- Created concept pages under `wiki/learning/concepts/`: `three-sources-of-meaning.md` (Frankl), `golden-circle.md` (Sinek), `inspire-vs-manipulate.md` (Sinek + Ariely), `social-vs-market-norms.md` (Ariely), `customer-development.md` (Blank).
- Updated MOC: `wiki/learning/index.md` — concepts grouped into Systems, Meaning, Leadership sub-sections; Books regrouped by theme; pending count 53 → 40.
- Synthesis: none new this batch. Existing `wiki/synthesis/sre-practice-for-bms.md` unaffected.
- Flipped `wiki_compiled: true` on 10 canonical sources + 3 Kindle re-sync duplicates (Sinek × 2, Gregg × 1).
- Sources processed (canonical):
  - `sources/learning/books/Kindle Highlights/Gaarder-Sophies World.md`
  - `sources/learning/books/Kindle Highlights/Frankl-Mans Search For Meaning.md`
  - `sources/learning/books/Kindle Highlights/Carnegie-How to Win Friends and Influence People.md`
  - `sources/learning/books/Kindle Highlights/Sinek-Start With Why.md`
  - `sources/learning/books/Kindle Highlights/Sinek-Leaders Eat Last.md`
  - `sources/learning/books/Kindle Highlights/Greene-The 48 Laws Of Power.md`
  - `sources/learning/books/Kindle Highlights/Ariely-Predictably Irrational.md`
  - `sources/learning/books/Kindle Highlights/Guillebeau-The $100 Startup.md`
  - `sources/learning/books/Kindle Highlights/Blank-The Four Steps to the Epiphany.md`
  - `sources/learning/books/Kindle Highlights/Mulcahy-The Gig Economy.md`
- Kindle re-sync duplicates also flipped (same content as canonical; not separately compiled):
  - `sources/learning/books/Kindle Highlights/Sinek-Start With Why-1720089033897.md`
  - `sources/learning/books/Kindle Highlights/Sinek-Leaders Eat Last-1720089017894.md`
  - `sources/learning/books/Kindle Highlights/Gregg-Systems Performance-1720089025892.md` (leftover from first batch)
- **Pending:** 40 source files remain with `wiki_compiled: false`. Still-pending Kindle re-sync dup to flag next pass: `Green-Turtles All the Way Down-1720089041995.md` (canonical not yet compiled; flip together when canonical runs).
- **Placeholder pages to re-densify on re-read:** Carnegie, Leaders Eat Last, $100 Startup — each had only one captured highlight.

## [2026-04-19 13:45] ingest-url (no args) — third compile batch
- Scope: 10 pending source files → 10 new book source-summary pages. Three dup flag-fixups from batch 2 closed out separately before this batch.
- Created book pages under `wiki/learning/books/`:
  - `tuesdays-with-morrie.md` (Albom)
  - `thirteen-reasons-why.md` (Asher, placeholder — 2 highlights)
  - `pride-and-prejudice.md` (Austen, placeholder — 4 highlights)
  - `and-every-morning-the-way-home.md` (Backman, placeholder — 3 highlights)
  - `origin.md` (Brown) — science-vs-religion, First Cause, the two questions
  - `the-da-vinci-code.md` (Brown) — symbology, divine proportion
  - `the-secret.md` (Byrne) — law of attraction + critique
  - `linux-for-beginners.md` (Cannon) — CLI, FHS, permissions lookup page
  - `and-then-there-were-none.md` (Christie, placeholder — 3 highlights)
  - `the-pilgrimage.md` (Coelho) — agape, fighting the good fight
- Created concept pages under `wiki/learning/concepts/`: `memento-mori.md` (Albom + Frankl + Backman), `law-of-attraction.md` (Byrne, with critique), `agape.md` (Coelho + Frankl), `fighting-the-good-fight.md` (Coelho), `divine-proportion.md` (Brown - Da Vinci Code), `unix-filesystem-hierarchy.md` (Cannon), `unix-file-permissions.md` (Cannon).
- Synthesis: `wiki/synthesis/linux-fundamentals-for-sre.md` (new, bridges Cannon → Gregg → SRE canon → BMS work — the four-step staircase).
- Updated MOCs: `wiki/learning/index.md` (Concepts regrouped into Systems/Meaning/Leadership/Ideas-with-asterisks; Books regrouped — new "Fiction" section; pending count 40 → 30), `wiki/synthesis/index.md` (added linux-fundamentals entry).
- Flipped `wiki_compiled: true` on all 10 canonical sources.
- Sources processed:
  - `sources/learning/books/Kindle Highlights/Albom-Tuesdays With Morrie.md`
  - `sources/learning/books/Kindle Highlights/Asher-Thirteen Reasons Why.md`
  - `sources/learning/books/Kindle Highlights/Austen-Pride and Prejudice.md`
  - `sources/learning/books/Kindle Highlights/Backman-And Every Morning the Way Home Gets Longer and Longer.md`
  - `sources/learning/books/Kindle Highlights/Brown-Origin.md`
  - `sources/learning/books/Kindle Highlights/Brown-The Da Vinci Code.md`
  - `sources/learning/books/Kindle Highlights/Byrne-The Secret.md`
  - `sources/learning/books/Kindle Highlights/Cannon-Linux for Beginners.md`
  - `sources/learning/books/Kindle Highlights/Christie-And Then There Were None.md`
  - `sources/learning/books/Kindle Highlights/Coelho-Sanches-The Pilgrimage.md`
- **Pending:** 30 canonical source files remain with `wiki_compiled: false`, plus 1 dup (`Green-Turtles All the Way Down-1720089041995.md`) awaiting its canonical (`Green-Turtles All the Way Down.md`) to be compiled — flip together next pass.
- **Placeholder pages to re-densify on re-read:** Thirteen Reasons Why (Asher), Pride and Prejudice (Austen), And Every Morning… (Backman), And Then There Were None (Christie) — plus carry-over from batch 2 (Carnegie, Leaders Eat Last, $100 Startup).
- **Observations:**
  - Fiction highlights (Asher, Austen, Backman, Christie) tended to be sparse — VB captured a few quotable lines rather than thematic density. Kindle-highlight-driven compilation works better for non-fiction.
  - Cannon's Linux book generated the strongest work-domain pull — extracted two concept pages and the Linux-fundamentals synthesis. When work/ gets populated, these concepts are prime candidates for domain-migration via `/lint-wiki`.
  - Brown's two novels (Origin, Da Vinci Code) share a science-vs-religion spine; cross-linked both directions.

## [2026-04-19 15:20] ingest-url (no args) — fourth compile batch
- Scope: 10 pending source files → 10 new book source-summary pages + 5 new concept pages. Heaviest-yield batch so far (Coelho + Collins trilogy + Green × 2 + Gilbert + Gray = dense extraction).
- Created book pages under `wiki/learning/books/`:
  - `the-alchemist.md` (Coelho) — Personal Legend; heart-listening; "world's greatest lie"
  - `the-hunger-games.md` (Collins) — silence as dissent
  - `catching-fire.md` (Collins) — Katniss interrogates her own motive; face-the-fight
  - `mockingjay.md` (Collins) — Panem et Circenses; Peeta's anti-war speech; Snow/Coin equivalence
  - `all-the-light-we-cannot-see.md` (Doerr) — radio as mass influence; snail-raft image; history-by-victors
  - `the-great-gatsby.md` (Fitzgerald, placeholder — 1 highlight)
  - `eat-pray-love.md` (Gilbert) — pleasure as obligation; soul-mate-as-mirror
  - `men-are-from-mars-women-are-from-venus.md` (Gray) — Mr. Fix-It trap, de-gendered
  - `looking-for-alaska.md` (Green) — labyrinth of suffering; forgiveness-as-survival
  - `turtles-all-the-way-down.md` (Green) — OCD spiral; "I am not my thoughts"; cites both canonical + dup source files
- Created concept pages under `wiki/learning/concepts/`:
  - `personal-legend.md` (Coelho) — maps to ikigai, Frankl's why, Sinek's WHY; counter-skepticism via law-of-attraction
  - `bread-and-circuses.md` (Juvenal / Collins / Doerr) — first political-economy concept page
  - `mr-fix-it-trap.md` (Gray, de-gendered) — listening-vs-solving; applied to 1:1s, code review, on-call
  - `labyrinth-of-suffering.md` (Green) — three proposed exits (deferral / cessation / forgiveness)
  - `intrusive-thoughts-vs-self.md` (Green + Gilbert) — CBT defusion; applied to on-call anxiety, imposter syndrome, blame loops
- Updated MOC: `wiki/learning/index.md` — new sub-sections "Communication & relationships" and "Political & social" in Concepts; 10 book entries added across Philosophy/Self-help/Fiction; pending count 30 → 20.
- Synthesis: none new. `mr-fix-it-trap` and `intrusive-thoughts-vs-self` have strong work/ affinity but filed under learning/ for now; candidates for `/lint-wiki` synthesis promotion once work/ populates.
- Flipped `wiki_compiled: true` on 10 canonical sources + 1 Kindle re-sync duplicate (`Green-Turtles All the Way Down-1720089041995.md` — its canonical compiled this batch; dup frontmatter cited alongside in the wiki page).
- Sources processed (canonical):
  - `sources/learning/books/Kindle Highlights/Coelho-The Alchemist.md`
  - `sources/learning/books/Kindle Highlights/Collins-The Hunger Games.md`
  - `sources/learning/books/Kindle Highlights/Collins-Catching Fire.md`
  - `sources/learning/books/Kindle Highlights/Collins-Mockingjay.md`
  - `sources/learning/books/Kindle Highlights/Doerr-All the Light We Cannot See.md`
  - `sources/learning/books/Kindle Highlights/Fitzgerald-The Great Gatsby.md`
  - `sources/learning/books/Kindle Highlights/Gilbert-Eat Pray Love.md`
  - `sources/learning/books/Kindle Highlights/Gray-Men Are from Mars, Women Are from Venus.md`
  - `sources/learning/books/Kindle Highlights/Green-Looking For Alaska.md`
  - `sources/learning/books/Kindle Highlights/Green-Turtles All the Way Down.md`
- Kindle re-sync duplicate flipped (same content as canonical; cited in wiki frontmatter):
  - `sources/learning/books/Kindle Highlights/Green-Turtles All the Way Down-1720089041995.md`
- **Pending:** 20 canonical source files remain with `wiki_compiled: false` in `sources/learning/books/Kindle Highlights/`. Re-run `/ingest-url` for the next batch.
- **Placeholder pages to re-densify on re-read:** Great Gatsby (Fitzgerald — 1 highlight) — plus carry-overs from earlier batches (Carnegie, Leaders Eat Last, $100 Startup, Thirteen Reasons Why, Pride and Prejudice, And Every Morning, And Then There Were None).
- **Observations:**
  - Turtles All the Way Down (58 highlights) was the single richest source of this batch — generated two concept pages and cross-linked into three others (labyrinth, memento-mori, three-sources-of-meaning).
  - Collins trilogy produced one concept page (`bread-and-circuses`) rather than three — each book reinforced a single political thesis. Book pages stand; concept is unified.
  - Gray's book required de-gendering before extraction — the underlying patterns (listen-vs-solve, advice-as-diagnosis) are sound; the Mars/Venus framing is not. Concept page notes the re-framing explicitly.
  - Still no `work/` pages created; pressure building on four concepts now (`unix-filesystem-hierarchy`, `unix-file-permissions`, `mr-fix-it-trap`, `intrusive-thoughts-vs-self`) that belong more in work/ than learning/.

## [2026-04-19 16:55] ingest-url (no args) — fifth compile batch
- Scope: 10 pending source files → 10 new book source-summary pages + 6 new concept pages. Dense batch: Lowndes (97 highlights), Hawking (35), Myers-Myers (26), Sharma (25), Niven (21), McGilchrist (19), Lee (17), Orwell (9), Rowell (4).
- Created book pages under `wiki/learning/books/`:
  - `a-brief-history-of-time.md` (Hawking) — falsifiability, anthropic principle, time as universe property
  - `siddhartha.md` (Hesse) — wisdom-cannot-be-passed-on; three competencies (think/wait/fast); river-as-eternal-present
  - `to-kill-a-mockingbird.md` (Lee) — Atticus's three claims: perspective-taking, conscience over majority, real courage
  - `how-to-talk-to-anyone.md` (Lowndes) — 90+ tactics digested; explicit rejection of "epoxy eyes" on ethical grounds
  - `the-master-and-his-emissary.md` (McGilchrist) — hemispheric attention; Master/Emissary parable as diagnostic
  - `gifts-differing.md` (Myers-Myers) — MBTI framework; reactions-to-change signature; explicit rejection of MBTI inventory for hiring
  - `all-the-bright-places.md` (Niven) — Waiting Place; "there is only now"; acceptance-of-loss; romanticization caveat
  - `animal-farm.md` (Orwell) — Squealer problem; four-line slide; engineering parallels
  - `eleanor-and-park.md` (Rowell, placeholder — 4 highlights)
  - `the-monk-who-sold-his-ferrari.md` (Sharma) — read critically as compressed cheat-sheet for material already in wiki from Hesse/Coelho
- Created concept pages under `wiki/learning/concepts/`:
  - `falsifiability.md` (Hawking via Popper) — the demarcation test; applications to SLOs, post-mortem hypotheses, architecture bets, PRDs
  - `hemispheric-attention.md` (McGilchrist) — narrow/focussed vs broad/vigilant; debugging=left, on-call=right; explicit rejection of pop-psych "left-brain/right-brain" personality talk
  - `mbti-perception-judgment.md` (Myers) — framework kept, inventory rejected; reactions-to-change as team lens
  - `perspective-taking.md` (Lee + Gray + Carnegie) — Atticus's move; not perspective-projecting; not sympathy; engineering applications (blameless post-mortems, code review, cross-team)
  - `wisdom-vs-knowledge.md` (Hesse + Polanyi) — operational claim about docs/pairing/shadowing
  - `first-impression-signals.md` (Lowndes distilled) — 4 load-bearing (flooding smile, sticky eyes, total-body turn, hang-by-your-teeth) + 4 amplifiers (mood match, comm-YOU-nication, echoing, limit-the-fidget); ethical calibration
- Updated MOC: `wiki/learning/index.md` — falsifiability added to Systems; wisdom-vs-knowledge added to Meaning; 4 new entries added to Communication & relationships (perspective-taking, first-impression-signals, mbti-perception-judgment, hemispheric-attention); 10 book entries added across Systems/Philosophy/Leadership/Fiction; pending count 20 → 9.
- Synthesis: none new. `falsifiability`, `hemispheric-attention`, `first-impression-signals` have strong work/ affinity but filed under learning/ for now; candidates for `/lint-wiki` synthesis promotion once work/ populates.
- Flipped `wiki_compiled: true` on all 10 canonical sources. No Kindle re-sync duplicates this batch.
- Sources processed (canonical):
  - `sources/learning/books/Kindle Highlights/Hawking-A Brief History Of Time.md`
  - `sources/learning/books/Kindle Highlights/Hesse-Siddhartha.md`
  - `sources/learning/books/Kindle Highlights/Lee-To Kill A Mockingbird.md`
  - `sources/learning/books/Kindle Highlights/Lowndes-How to Talk to Anyone.md`
  - `sources/learning/books/Kindle Highlights/McGilchrist-The Master and His Emissary.md`
  - `sources/learning/books/Kindle Highlights/Myers-Myers-Gifts Differing.md`
  - `sources/learning/books/Kindle Highlights/Niven-All the Bright Places.md`
  - `sources/learning/books/Kindle Highlights/Orwell-Animal Farm.md`
  - `sources/learning/books/Kindle Highlights/Rowell-Eleanor & Park.md`
  - `sources/learning/books/Kindle Highlights/Sharma-The Monk Who Sold His Ferrari.md`
- **Pending:** 9 canonical source files remain with `wiki_compiled: false` in `sources/learning/books/Kindle Highlights/`. Re-run `/ingest-url` for the next batch.
- **Placeholder pages to re-densify on re-read:** Eleanor & Park (Rowell — 4 highlights) — plus carry-overs (Great Gatsby, Carnegie, Leaders Eat Last, $100 Startup, Thirteen Reasons Why, Pride and Prejudice, And Every Morning, And Then There Were None).
- **Observations:**
  - Lowndes's 97 highlights were the single richest source of the batch — distilled into one book page + one dense concept page with explicit discards (epoxy eyes, gendered framings, fake stats).
  - Two books here required a *critical* rather than summarising compile: Myers-Myers (framework yes, MBTI instrument no) and Sharma (useful compression but not load-bearing where Hesse/Coelho already cover the ground). Both pages flag what to trust and what to skip.
  - Hawking's `falsifiability` is the batch's most portable engineering concept — applies to SLOs, RCAs, architecture decisions, PRDs. Strong candidate for promotion to `synthesis/` or migration to `work/` once that domain populates.
  - Carry-over: `work/` still unpopulated; seven concepts now have work-domain affinity (unix-*, mr-fix-it-trap, intrusive-thoughts-vs-self, falsifiability, hemispheric-attention, first-impression-signals). `/lint-wiki` should flag the growing pile.

## [2026-04-19 18:30] ingest-url (no args) — sixth compile batch (Kindle corpus complete)
- Scope: final 9 pending Kindle source files → 9 new book source-summary pages + 5 new concept pages. Mixed batch: Zafón (60 highlights) and Yoon (45) were dense; Todd (3), Tuhovsky (2), Watt (2), Walton (4) were placeholder-thin; Yogananda (9), Zusak (11), Thomas (26) sat in between.
- Created book pages under `wiki/learning/books/`:
  - `thomas-the-big-switch.md` (Thomas) — career-change fable; quiet-desperation operationalised; Coelho/Sharma compressed
  - `todd-after.md` (Todd, placeholder — 3 highlights)
  - `tuhovsky-communication-skills-training.md` (Tuhovsky, placeholder — 2 fragmentary highlights)
  - `walton-emotional-intelligence.md` (Walton, thin) — one load-bearing fragment: behavioural templates → samskaras concept
  - `watt-mindfulness.md` (Watt, short) — panning-camera scan exercise; ties to right-mode attention
  - `yogananda-bhagavad-gita.md` (Yogananda) — karma yoga; samskaras; body-as-kingdom; Changelessness; explicit bracket of tradition-specific metaphysics
  - `yoon-the-sun-is-also-a-star.md` (Yoon) — determinism vs fate as running argument; lust/attraction/attachment; Sagan's apple pie
  - `zafon-shadow-of-the-wind.md` (Zafón) — books-as-mirrors; secrecy-is-relational; prisons-of-words; post-war shroud of silence
  - `zusak-the-book-thief.md` (Zusak) — not-leaving as love; every-pattern-tips; words-as-clouds; Death-narrator acknowledgment that captured highlights are sparse
- Created concept pages under `wiki/learning/concepts/`:
  - `karma-yoga.md` (Yogananda) — full engagement + non-attachment to outcome; de-sectarianised; applied to on-call, migrations, perf reviews
  - `samskaras.md` (Yogananda + Walton) — behavioural templates; same mechanism in Eastern + Western registers; applied to on-call reflex-building and toil
  - `quiet-desperation.md` (Thomas via Thoreau) — 5-point symptom cluster; 4-step exit; not-every-dissatisfaction-is-this
  - `coincidence-vs-narrative.md` (Yoon + Zafón) — story-generator vs null-tester; three regimes (coincidence, common cause, causal); post-incident narrative smoothing hazard
  - `books-as-mirrors.md` (Zafón) — reader projects onto text; re-reading is a different book; diverse reviewers catch more bugs
- Updated MOC: `wiki/learning/index.md` — 3 new concepts in Meaning (karma-yoga, samskaras, quiet-desperation); 1 in Communication (books-as-mirrors); 1 in Ideas with asterisks (coincidence-vs-narrative); 9 book entries added across Philosophy/Leadership/Fiction; pending count 9 → 0 (footer updated to reflect Kindle corpus completion).
- Synthesis: none new. `karma-yoga`, `samskaras`, `coincidence-vs-narrative` all have strong work/ affinity — prime candidates for synthesis promotion once work/ populates.
- Flipped `wiki_compiled: true` on all 9 canonical sources. No Kindle re-sync duplicates this batch.
- Sources processed (canonical):
  - `sources/learning/books/Kindle Highlights/Thomas-The Big Switch.md`
  - `sources/learning/books/Kindle Highlights/Todd-After.md`
  - `sources/learning/books/Kindle Highlights/Tuhovsky-Editing-Communication Skills Training.md`
  - `sources/learning/books/Kindle Highlights/Walton-A Practical Guide to Emotional Intelligence.md`
  - `sources/learning/books/Kindle Highlights/Watt-A Practical Guide to Mindfulness.md`
  - `sources/learning/books/Kindle Highlights/Yogananda-God Talks with Arjuna The Bhagavad Gita.md`
  - `sources/learning/books/Kindle Highlights/Yoon-The Sun is also a Star.md`
  - `sources/learning/books/Kindle Highlights/Zafon-The Shadow Of The Wind.md`
  - `sources/learning/books/Kindle Highlights/Zusak-The Book Thief.md`
- **Pending:** 0 canonical source files remain with `wiki_compiled: false`. Kindle highlights corpus (63 books) fully compiled across batches 1–6. Next ingest runs will process `inbox/urls.md`, newly-added source files, or `/ingest-file <path>` arguments.
- **Placeholder pages across all batches to re-densify on re-read:** Great Gatsby (Fitzgerald), Carnegie, Leaders Eat Last, $100 Startup, Thirteen Reasons Why, Pride and Prejudice, And Every Morning (Backman), And Then There Were None (Christie), Eleanor & Park (Rowell), After (Todd), Communication Skills Training (Tuhovsky).
- **Observations:**
  - The Kindle corpus total stats: 63 source files → 48 non-placeholder book pages + 11 placeholders + 30 concept pages + 2 synthesis pages. Concept-per-book ratio ~0.5; the dense sources (Lowndes, Kleppmann, DDIA, Turtles, Gita, Zafón) carried most of the concept weight.
  - This batch's reach-into-engineering concepts: **karma yoga** (on-call attitudinal discipline), **samskaras** (template-hygiene against bad on-call reflexes), **coincidence vs narrative** (post-mortem anti-smoothing discipline). All three are strong work/ promotion candidates.
  - Quiet desperation is a useful frame specifically because engineering comp structures + well-defined roles make it easy to *stay* in misaligned work past the point where exit would be the right move.
  - Zafón's "prisons of words" cluster feeds directly into how wiki/work/ should approach written feedback (code review, perf reviews, 1:1 notes) when that domain populates.
  - `/lint-wiki` should now flag the growing work-domain-affinity pile (10+ concepts) and the fact that work/ remains structurally empty despite the ingestion being book-oriented — the bridge is ready; the other side needs material.
  - Next natural step: populate work/ from Confluence/BMS sources, or add new URL-based ingests via `inbox/urls.md`.

## [2026-04-19 00:00] schema-update — 60% highlight-coverage rule
- Updated: `CLAUDE.md` (added coverage rule + placeholder exemption to `/ingest-url` section; added lint check for sub-60% pages)
- Updated: `.claude/commands/ingest-url.md` (Compile step now enforces 60% rule with "Other notable passages" pattern)
- Rationale: the fixed "3–8 concepts per source" target did not scale with source density — a 97-highlight book and a 10-highlight book got similar cite-counts, so dense books dropped more material proportionally. The 60% rule makes coverage track source density while preserving distilled-voice discipline via the "Other notable passages" grouping (one interpretive sentence per cluster, 2–5 grouped `loc X` citations).
- Note: **Batches 7+ are recompiles, not new ingests.** They retrofit existing book pages to meet the new 60% rule. Placeholders (books with <5 source highlights — Carnegie, Leaders Eat Last, $100 Startup, Thirteen Reasons Why, Pride and Prejudice, And Every Morning, And Then There Were None, Gatsby, Eleanor & Park, After, Tuhovsky) are exempt and remain unchanged.

## [2026-04-19 01:00] recompile batch 7 — densest 8 books to 60% coverage
- Scope: 8 book pages retrofitted with an "Other notable passages" section, each cluster carrying a one-sentence interpretive frame and 2–5 grouped `loc X` citations. Load-bearing sections preserved byte-for-byte.
- Updated pages + final distinct-loc counts vs target (ceil(0.6 × N)):
  - `wiki/learning/books/how-to-talk-to-anyone.md` — 65 / 59 (N=97)
  - `wiki/learning/books/start-with-why.md` — 56 / 51 (N=85)
  - `wiki/learning/books/origin.md` — 64 / 45 (N=74)
  - `wiki/learning/books/zafon-shadow-of-the-wind.md` — 45 / 36 (N=60)
  - `wiki/learning/books/systems-performance.md` — 56 / 36 (N=59)
  - `wiki/learning/books/turtles-all-the-way-down.md` — 45 / 35 (N=58)
  - `wiki/learning/books/the-da-vinci-code.md` — 39 / 30 (N=50)
  - `wiki/learning/books/yoon-the-sun-is-also-a-star.md` — 38 / 27 (N=45)
- No new wiki pages created, no concept-page edits, no MOC edits, no source modifications.
- **New-concept candidates surfaced (not created — parked for future `/ingest-url --force` passes):**
  - Lowndes: `horse-sense-dual-tracking`, `broken-record-boundary`, `big-cats-vocabulary-register`.
  - Sinek: `why-types-vs-how-types`, `cathedral-vs-wall`, `discovery-not-invention`, `symbols-carry-meaning`.
  - Brown/Origin: `the-regent-problem`, `first-cause-regress`, `kirsch-bibliography`, `syncretism`.
  - Gregg: `use-method` (stub-exists-needs-flesh), `observer-effect`, `dynamic-tracing-taxonomy`.
  - Green/Turtles: `involuntary-cognition`, `borrowed-vocabulary-for-pain`, `wealth-as-cage` (candidate learning↔finances synthesis).
  - Brown/Da Vinci: `atbash-cipher`, `sacred-feminine-thesis`, `opus-dei`, `nag-hammadi-dead-sea-scrolls`.
  - Yoon: `36-questions-protocol`, `falling-vs-choosing`, `identity-as-inheritance`; synthesis `defensible-vs-correct`.
  - Zafón: `parents-as-first-compiler`, `vocation-as-hiding-place`, `survivors-ledger`, `love-is-diagnosed-not-declared`.
- Edge cases surfaced by agents:
  - Zafón page was already at 19 outgoing wikilinks (over the 15 cap from prior compile); recompile added zero new wikilinks, kept all new coverage as `loc X` citations only. The pre-existing 19 remains over-budget and needs a `/lint-wiki` trim pass later.
  - Several pages (Origin, Da Vinci Code, Yoon, Turtles, Systems Performance) had no pre-existing "What to skip" or "For engineering contexts" sections; agents placed the new section before "Related" instead — behaviour consistent with the plan's "whichever fits each page's existing shape".
  - Re-sync duplicate sources for Gregg and Green were byte-identical in highlight content; no extra material harvested.
  - A handful of highlights were legitimately skipped as single-word vocabulary fragments (e.g., `copacetic`, `entropy`, `reverence`, `syncretism` as bare terms) — not counted against coverage.

## [2026-04-19 02:00] recompile batch 8 — medium-density 8 books to 60% coverage
- Scope: 8 more book pages retrofitted with `## Other notable passages` sections.
- Updated pages + final distinct-loc counts vs target (strict lint regex: each loc number carries its own `loc` prefix):
  - `wiki/learning/books/designing-data-intensive-applications.md` — 38 / 27 (N=44)
  - `wiki/learning/books/tuesdays-with-morrie.md` — 34 / 24 (N=40)
  - `wiki/learning/books/a-brief-history-of-time.md` — 29 / 21 (N=35)
  - `wiki/learning/books/site-reliability-engineering.md` — 24 / 20 (N=32)
  - `wiki/learning/books/sophies-world.md` — 37 / 31 (N=51)
  - `wiki/learning/books/the-alchemist.md` — 23 / 17 (N=28)
  - `wiki/learning/books/the-pilgrimage.md` — 21 / 17 (N=27)
  - `wiki/learning/books/siddhartha.md` — 19 / 17 (N=27)
- Citation-format normalisation: grouped citations like `(loc 1683, 1687)` were normalised to `(loc 1683, loc 1687)` on pages where the strict single-loc regex would otherwise miss the second number (Siddhartha, preemptively). Future recompiles should prefer the explicit `loc N, loc N` form so `/lint-wiki`'s coverage audit counts every number.
- **New-concept candidates surfaced (parked):**
  - Kleppmann/DDIA: `head-of-line-blocking`, `schema-on-read-vs-schema-on-write`, `declarative-vs-imperative-queries`, `oltp-vs-olap-storage`, `impedance-mismatch`.
  - Albom/Morrie: `tension-of-opposites`, `love-or-perish-auden`, `daily-memento-mori-ritual`, `suffering-as-solvent`.
  - Hawking: `singularity`, `quantum-uncertainty`, `light-cones`, `wave-particle-duality`, `dirac-equation`.
  - Gaarder/Sophie: `wonder-as-faculty`, `naturalism-vs-myth`, `nature-vs-convention-nomos`.
- No new concept pages created, no MOC edits, no source modifications. All load-bearing sections preserved byte-for-byte; Other-notable-passages inserted before the nearest downstream section (`For engineering contexts`, `For VB`, `Connections`, `Related`, or `Source` depending on the page).

## [2026-04-19 03:00] recompile batch 9 — 8 more medium-density books
- Updated pages + final distinct-loc counts vs target:
  - `wiki/learning/books/thomas-the-big-switch.md` — 24 / 16 (N=26)
  - `wiki/learning/books/gifts-differing.md` — 19 / 16 (N=26)
  - `wiki/learning/books/all-the-bright-places.md` — 16 / 13 (N=21)
  - `wiki/learning/books/the-monk-who-sold-his-ferrari.md` — 20 / 15 (N=25)
  - `wiki/learning/books/the-master-and-his-emissary.md` — 15 / 12 (N=19)
  - `wiki/learning/books/men-are-from-mars-women-are-from-venus.md` — 14 / 10 (N=16)
  - `wiki/learning/books/eat-pray-love.md` — 17 / 12 (N=20)
  - `wiki/learning/books/to-kill-a-mockingbird.md` — 12 / 11 (N=17)
- **Pre-existing cap violation flagged by batch-9 agents:** `thomas-the-big-switch.md` carries 21 outgoing wikilinks (pre-recompile); agents added zero new links, so the violation is inherited from first-compile. `/lint-wiki` should surface it for a trim pass — candidate links to drop: duplicate entries from the same book cluster, or move 1–2 into the page body text instead of the Related footer.
- **Grouped-citation artefact:** `the-monk-who-sold-his-ferrari.md` has a pre-existing `loc 740, 741, 742` grouped citation (strict-regex counts only `740`); left untouched per invariant #1. Page still clears target with 19 distinct source citations without normalising it.
- New-concept candidates parked: `mbti-type-dynamics-inferior-function`, `rewards-blindness`, `situational-anchoring-interior-weather`, `attention-shapes-world` (already has page — verify), `atticus-moral-courage`.



## [2026-04-19 recompile] origin (Brown) — 60% coverage retrofit
- Updated: `wiki/learning/books/origin.md` — added "Other notable passages" section (6 thematic clusters) between "Aphorisms" and "Related".
- Coverage: 72 of 74 source highlights now cited (up from 19) — 97.3%, well past the 60% threshold. Only loc 7217 ("syncretism", a single-word term drop) remains uncited.
- Preserved byte-for-byte: lede, "The two driving questions," "Brown's framing of science vs. religion," "Scientific ideas threaded through the plot," "Aphorisms," "Related."
- Clusters: interfaith triad + opening provocation; setting-as-argument; supporting cast; the assassin's theology (Ávila); thriller mechanics + Kirsch's bibliography; humanist register (Nietzsche-through-Churchill-to-love-aphorisms).
- Wikilinks: 4/15 (unchanged — preferred loc citations over new links, per schema).
- Source: `sources/learning/books/Kindle Highlights/Brown-Origin.md` (unchanged; immutable).

## [2026-04-19 recompile] the-pilgrimage (Coelho) — 60% coverage retrofit
- Updated: `wiki/learning/books/the-pilgrimage.md` — added "Other notable passages" section (5 thematic paragraphs) between "Aphorisms" and "Related".
- Coverage: 25 of 27 source highlights now cited (up from 15) — 92.6%, well past the 60% threshold. Uncited: loc 1142 (light/daylight aphorism), loc 1857 (duplicate "we create the pace of time").
- Preserved byte-for-byte: lede, "Central teachings" subsections, "Aphorisms," "Related."
- Clusters: the Road as teacher; dreams as soul-food + self-cruelty diagnostic; love distorted (eros/philia/agape fracture); fear as the real enemy on the Road; conviction without conversion.
- Wikilinks: 10/15 (re-used existing `../concepts/agape` — no new link-budget spend).
- Source: `sources/learning/books/Kindle Highlights/Coelho-Sanches-The Pilgrimage.md` (unchanged; immutable).

## [2026-04-19 recompile] mockingjay coverage
- Recompiled `wiki/learning/books/mockingjay.md` to satisfy 60% highlight-coverage rule.
- Coverage: 18 of 18 source highlights cited (100%, up from 8/18 = 44%).
- Added `## Other notable passages` with 3 thematic paragraphs (symbol-making; solitude/stone/deception; republic + Buttercup parable) — 10 newly cited locs: 54, 64, 132, 553, 711, 729, 921, 1287, 1638, 2230.
- Preserved byte-for-byte: lede, "The core political concept," anti-war speech, Snow vs. Coin, collective memory, healing-not-fire, "Aphorisms," "Related."
- Wikilinks: 8/15.
- Source: `sources/learning/books/Kindle Highlights/Collins-Mockingjay.md` (unchanged; immutable).

## [2026-04-19 recompile] all-the-light-we-cannot-see (Doerr) — 60% coverage retrofit
- Updated: `wiki/learning/books/all-the-light-we-cannot-see.md` — added "Other notable passages" section (3 thematic paragraphs) before "Related".
- Coverage: 12 of 15 source highlights cited (80%, well past 60% threshold). Newly cited: loc 876, 1888, 1903. Uncited fragments: loc 1934–1935 (the Nathan Hale quote spread across 3 ref fragments — treated as a single quote, not load-bearing).
- Preserved byte-for-byte: lede, "The book's central question," "Radio as mass influence," "History is victors'-written," "Obstacles as opportunity," "The snail raft," "Aphorisms," "Related."
- Clusters: war's collapsing rationalizations (876); radio as pedagogy counter-note to propaganda (1888); fear as unseen light (1903).
- Wikilinks: 4/15 (unchanged — no new links spent).
- Source: `sources/learning/books/Kindle Highlights/Doerr-All the Light We Cannot See.md` (unchanged; immutable).

## [2026-04-19 04:00] recompile batch 10 — 8 small-gap books to 60% coverage
- Scope: 8 small-to-medium source pages retrofitted with `## Other notable passages` sections; all cleared target.
- Updated pages + final distinct-loc counts vs target:
  - `wiki/learning/books/mockingjay.md` — 18 / 11 (N=18)
  - `wiki/learning/books/catching-fire.md` — 13 / 8 (N=13)
  - `wiki/learning/books/the-hunger-games.md` — 11 / 8 (N=12)
  - `wiki/learning/books/zusak-the-book-thief.md` — 11 / 7 (N=11)
  - `wiki/learning/books/the-gig-economy.md` — 17 / 11 (N=17)
  - `wiki/learning/books/mans-search-for-meaning.md` — 6 / 5 (N=8; frontmatter says 5, ^ref count = 8 — used 8 as authoritative)
  - `wiki/learning/books/the-four-steps-to-the-epiphany.md` — 18 / 11 (N=18)
  - `wiki/learning/books/all-the-light-we-cannot-see.md` — 11 / 9 (N=15)
- Note: per-page entries for `mockingjay.md` and `all-the-light-we-cannot-see.md` were appended by their sub-agents above — this entry is the batch summary only.
- **New-concept candidates parked for future passes:**
  - Collins/Hunger Games trilogy: `symbol-making-vs-symbol-breaking`, `involuntary-dissent`, `register-as-power`, `republic-vs-regime`, `buttercup-parable`.
  - Zusak: `not-leaving-as-love` (already touches `agape`), `pattern-tipping-point`, `invisibility-in-crowd`.
  - Mulcahy/Gig Economy: `bimodal-income-shape`, `portfolio-career-as-default`, `personal-vision-as-quarterly-ritual`.
  - Frankl: `existential-vacuum`, `logotherapy-three-doors` (meaning via work / love / attitude), `tragic-optimism`.
  - Blank/Four Steps: `customer-discovery-vs-execution`, `validation-milestone-gates`, `burn-rate-discipline`, `chasm-model`.
  - Doerr/Light: `radio-as-counter-pedagogy`, `fear-as-unseen-light`, `rationalisations-of-war`.
- Edge cases:
  - `the-hunger-games.md` agent reported 12 final locs but strict grep shows 11 — off-by-one but still clears target 8. No further action.
  - `mans-search-for-meaning.md`: source `highlightsCount: 5` in frontmatter but `^ref-` grep returned 8 unique refs — treated 8 as authoritative; target = ceil(0.6×8) = 5; page clears with 6.
  - No wikilink-cap violations introduced; no concept pages created; no sources modified.

## [2026-04-19 05:00] recompile batch 11 — 3 remaining small-gap books
- Scope: three pages short of the 60% target by 1–2 citations; each retrofitted with a small `## Other notable passages` insertion.
- Updated pages + final distinct-loc counts vs target:
  - `wiki/learning/books/animal-farm.md` — 10 / 6 (N=9)
  - `wiki/learning/books/the-secret.md` — 12 / 8 (N=13)
  - `wiki/learning/books/looking-for-alaska.md` — 17 / 14 (N=22) *(strict grep reports 18, but one `loc 1694` is a cross-reference to a Morrie loc — 17 Alaska-source locs)*
- **New-concept candidates parked:**
  - Orwell/Animal Farm: `coerced-volunteerism` (loc 655 — "strictly voluntary but rations halved"; maps cleanly onto SRE on-call / weekend-deploy pathology — candidate learning↔work synthesis).
  - Byrne/The Secret: `locus-of-control-vs-magical-agency`, `abundance-as-infinite-resource-fallacy` (both critical extensions of an existing `[[law-of-attraction]]` concept).
  - Green/Looking for Alaska: `second-death-memory-decay` (loc 2969), `complicity-without-certainty` (loc 3202/3296). `deferred-life-syndrome` already has a loc citation but could be promoted to a standalone page.
- No sources modified, no concept pages created, no wikilink-cap violations introduced.

## [2026-04-19 12:00] recompile — the-millionaire-fastlane (60% coverage retrofit)
- Scope: largest book page in the vault (source `highlightsCount: 295`). Pre-retrofit distinct-loc count was 2; target = ceil(0.6 × 295) = 177.
- Updated page + final distinct-loc count vs target:
  - `wiki/learning/books/the-millionaire-fastlane.md` — 292 / 177
- Additive only: all five existing sections (Core argument, The three roadmaps, Key concepts, Personal-note additions, Source references) preserved byte-for-byte. A new `## Other notable passages` section inserted between Personal-note additions and Source references, organised into 14 thematic clusters of 15–25 citations each (slightly above the 8–12 suggestion but each cluster is a discrete section of DeMarco's actual argument structure).
- Cluster titles: Process over events; Polluted vocabulary / faux wealth; Sidewalk mechanics; Victimhood and responsibility; Slowlane math (5-for-2); Uncontrollable Limited Leverage; Slowlane dangers; Fastlane as producer OS; Money trees and the five seedlings; Law of Effection; Choice as horsepower; Headwinds + time as king + education hack; Commitment, Redline, intelligent risk; CENTS filter + open-road spotting; Three Fastlane interstates.
- Source N was 295 highlights but the source contains 293 unique loc numbers (two duplicates — `3175` is the most visible, where DeMarco repeats a passage about forks in the road). Coverage math uses the 295 denominator per spec; 292 unique cited locs covers ~99% regardless.
- **New-concept candidates parked (NOT created):**
  - `paradox-of-practice` (loc 1903, loc 1986) — gurus teaching one wealth equation while getting rich in another; useful lens for evaluating finance influencers and SRE thought-leaders alike.
  - `indentured-time-vs-free-time` (loc 3518, loc 3523, loc 3530) — sharper than the existing time-budget framing; could anchor a finances↔learning synthesis with FIRE-adjacent concepts.
  - `horsepower-of-choice` (loc 3148, loc 3157, loc 3180) — asteroid-trajectory metaphor for why youthful compounding (decisions, not just money) is numerically different from late-career compounding.
  - `producer-vs-consumer-switch` (loc 2350, loc 2357, loc 2359) — the team-switch framing; near-miss with the existing `[[../../finances/concepts/wealth-equation]]` but stands on its own as a mental model.
  - `law-of-effection` (loc 2876, loc 2942) — already implicit in CENTS/Scale but could be promoted as its own concept page linking to Effection-style ideas in other books.
  - `cents-framework-entry-barrier-subrule` (loc 4153, loc 4157, loc 4229) — the "low entry = saturation" subrule already lives inside the CENTS page, but the Entry commandment might deserve its own atomic page given how often it gets invoked.
- Edge cases:
  - Sparse-section risk: clusters 10 (Effection) and 14 (interstates) are 9 and 7 citations, below the 15–25 target; kept tight rather than padding with off-theme locs. Other clusters all within the 15–25 band.
  - Existing citations `loc 638` (Core argument) and `loc 704` (Core argument) deliberately NOT re-cited in the new section to keep cluster themes clean; the distinct-loc count still clears target by a wide margin.
  - No single-word vocabulary fragments (e.g. `loc 1648` "Uncontrollable Limited Leverage,") were skipped — they're cited inside their thematic cluster even when the highlighted text is a phrase not a sentence.
  - No wikilinks added beyond the existing four; the CENTS concept page was referenced inside the CENTS cluster (already-linked target so no budget consumed).
  - No sources modified; no concept pages created; `status: draft` retained (promotion to `live` is a separate decision).

## [2026-04-19 06:00] Phase 7 audit — 60% coverage pass verified across entire books shelf
- Ran Grep-based distinct-`loc N` count against source `highlightsCount` on all 58 pages in `wiki/learning/books/`.
- **Result:** zero SHORT pages. All non-placeholder Kindle-source books clear `ceil(0.6 × N)`. All placeholders (N<5) correctly exempt.
- Distribution:
  - **42 Kindle-source books — OK.** From sparse (`mans-search-for-meaning` 6/3, N=5 edge case) to densest (`the-millionaire-fastlane` 292/177, N=295; `how-to-talk-to-anyone` 65/59, N=97; `origin` 64/45, N=74).
  - **14 placeholders — exempt.** Carnegie, Sinek/Leaders-Eat-Last, Guillebeau, Asher, Austen, Backman, Christie, Fitzgerald, Rowell, Todd, Tuhovsky, Watt, Walton, Xu.
  - **2 non-Kindle pages — outside rule scope.** `ikigai.md` and `the-million-dollar-weekend.md` are inlined personal-notes sources with no `loc N`-citable Kindle highlights.
- Carry-over items (not in scope for this retrofit; tracked for `/lint-wiki`):
  - `thomas-the-big-switch.md` 21 outgoing wikilinks (over 15-cap, pre-existing).
  - `zafon-shadow-of-the-wind.md` 19 outgoing wikilinks (over 15-cap, pre-existing).
  - Grouped-citation format `(loc N, N)` still present on `the-monk-who-sold-his-ferrari.md` (pre-existing; lint regex undercounts but page clears target anyway).
  - ~20 new-concept candidates surfaced across batches 7–11 and the DeMarco outlier — parked; not created this pass per plan's "not adding new concept pages" non-goal.
- **The 60% highlight-coverage retrofit is complete.** Schema (`CLAUDE.md` + `ingest-url` skill) has been updated so future first-compiles honor the rule natively.
