---
description: Classify items in inbox/ and propose where they belong in the wiki
argument-hint: "[--auto-approve-high-confidence]"
---

You are running the `/process-inbox` command. Read `CLAUDE.md` at the vault root first.

## Execution logic

1. **List every file in `inbox/`** except:
   - `inbox/urls.md` (handled by `/ingest-url` without args)
   - `inbox/review/` (holds user-deferred items — skip unless explicitly targeted)
2. **For each file:**
   - Read the content.
   - Classify the domain using `CLAUDE.md` rules.
   - Decide: (a) **create new wiki page** or (b) **merge into existing wiki page**.
   - If merging, identify the target page by searching `wiki/<domain>/` for conceptual matches.
3. **Present a plan** to the user, grouped by domain, e.g.:
   ```
   inbox/ — 7 items pending

   work (2):
     1. idea-for-chaos-engineering.md → merge into wiki/work/chaos-engineering.md
     2. meeting-random-thought.md     → new wiki/work/bms-release-process.md

   finances (3):
     3. sip-thought.md                → merge into wiki/finances/sip-strategy.md
     4. tax-saving-idea.md            → new wiki/finances/tax-optimization.md
     5. crypto-vs-stocks.md           → new wiki/finances/crypto-vs-stocks.md

   learning (1):
     6. rag-vs-wiki-thought.md        → merge into wiki/learning/llm-wiki-pattern.md

   review (1):
     7. vague-thought.md              → too ambiguous; move to inbox/review/
   ```
4. **Wait for user approval** per group or per-item. Never bulk-move without confirmation unless `--auto-approve-high-confidence` is passed AND confidence is above 0.85 for that item.
5. **Execute approved moves:**
   - Merging: append content to target wiki page under a new `## <date> — from inbox` section, update `updated:` frontmatter, link to relevant MOC.
   - New page: create with proper frontmatter, ensure at least one MOC link and one sibling link.
6. **On successful merge/move,** delete the original from `inbox/` (or move to `.trash/` if the item was substantial).
7. **Append to `wiki/log.md`:**
   ```markdown
   ## [<YYYY-MM-DD HH:MM>] process-inbox (<N> items)
   - Merged: <list>
   - Created: <list>
   - Deferred to review: <list>
   ```

## Guardrails

- If an item is <30 characters and offers no clear signal → propose `inbox/review/` or `.trash/`.
- If the user rejects a routing decision, remember the correction for this session (don't propose the same wrong routing twice).
- Never merge content from inbox into a `source-summary` type page — those summarize external material, not inbox thoughts.
