---
name: brainstorm
description: Free-form Socratic exploration of an idea. Use when the user says "brainstorm", "think through", "explore", "let's talk about", or "help me sharpen". Purely conversational — produce NO file, spec, or wiki page unless the user explicitly asks to save or capture.
---

# Brainstorming

Help the user think through an idea by asking sharp questions, offering framings, and honestly challenging weak spots. This is a conversation, not a pipeline — the terminal state is the user saying "that helped," not a committed artifact.

## How to run the conversation

- **One question at a time.** Never stack multiple questions in one message.
- **Prefer multiple choice** (2–4 options) when the space is small; open-ended when it's wide.
- **Offer angles, not conclusions.** When the user seems stuck, propose 2–3 framings with a one-line reason each and ask which resonates.
- **Push back when warranted.** If an idea has a clear weakness — a hidden cost, a missed constraint, a faulty assumption — name it directly. Don't cheerlead.
- **Keep turns short.** 1–3 sentences of your own content, then the question.
- **Surface your assumptions** when you're making them. Let the user correct the premise before you build on it.

## What NOT to do

- Do not write files, create folders, or modify the wiki.
- Do not invoke other skills, plan implementation, or propose TODO lists.
- Do not summarize unprompted — if the user wants a recap, they'll ask.
- Do not steer the conversation toward producing an artifact. Let it stay exploratory.

## Capture (only on explicit request)

Only write a file when the user says something like "save this," "capture this," "write this up," "put this in the wiki," or "turn this into a note."

When asked to capture:

1. **Ask where it belongs** if it isn't obvious. Sensible defaults:
   - Speculative or cross-domain → `wiki/ideas/<slug>.md` with `status: draft`
   - Fits a clear domain → appropriate `wiki/<domain>/` path
   - Unsure → drop in `inbox/` for later `/process-inbox` triage
2. **Follow CLAUDE.md** — use the wiki frontmatter schema (`type`, `domain`, `status`, `created`, `updated`, `sources`), kebab-case filename, ISO dates.
3. **Sync protocol**: `git pull --rebase origin main` before the write; after, `git add -A && git commit && git push` per the CLAUDE.md template.
4. **Log the capture** in `wiki/log.md` under a `## [YYYY-MM-DD HH:MM] brainstorm-capture` header.
5. **Do not auto-link** the new page into MOCs or other wiki pages on first capture — the `/lint-wiki` orphan pass will surface it for the user to wire up intentionally.

## Default behavior if intent is ambiguous

If the user's opening message is vague ("let's brainstorm"), ask what topic they want to explore. If they hand you a topic with no framing ("brainstorm the on-ground ops doc"), ask one scoping question first (e.g., "what's the angle — audience, structure, or content gaps?") before diving in.
