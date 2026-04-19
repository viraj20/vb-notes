---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Hesse-Siddhartha.md
---

# Wisdom vs knowledge

Parent: [[../index|Learning MOC]]

[[../books/siddhartha|Hesse's]] distinction (loc 1681, 1683, 1687):

> "Wisdom cannot be passed on. Wisdom that a wise man attempts to pass on to someone always sounds like foolishness."

> "Knowledge can be transferred, but not wisdom."

> "Any truth can only be expressed and put into words when it is one-sided. Everything that can be thought with the mind and said with words is one-sided, lacking completeness, roundness, or unity."

Knowledge is what you can say. Wisdom is what you can only *be*. The claim survives outside Hesse's register — it matches several careful traditions (rabbinic distinction between *da'at* and *binah*, Confucian *zhi* vs *ming*, Polanyi's tacit-vs-explicit) and a lot of engineering experience.

## The operational claim

Three things follow from Hesse's distinction:

1. **Documents transfer knowledge, not wisdom.** A runbook can tell you what to check; it cannot tell you when the system is lying to you. The latter is wisdom — pattern-matching on underdetermined signals — and it is a product of experience, not writing.
2. **Wisdom must be re-earned.** You cannot give it to the next on-call, no matter how many post-mortems you link. They will learn it by being the next on-call. What you *can* give them is more signals, better tools, and faster feedback — the scaffolding that accelerates the re-earning.
3. **Teaching wisdom directly backfires.** Hesse: it "sounds like foolishness." A senior engineer who tries to *tell* a junior the thing they learned the hard way usually produces resentment, not competence. The things wisdom can teach are: the existence of the thing, how to notice when you need it, where to look.

## Why the distinction matters for engineering documentation

A tempting mistake: treat the on-call runbook as a transfer vehicle for on-call wisdom. It isn't. Runbooks transfer the *knowledge* layer — here are the dashboards, here are the common failure modes, here are the escalation paths. The *wisdom* layer — "this alert looks real but is almost certainly a side-effect of X" — cannot be runbook-ed. It can be *named in the runbook* so the next person knows to look for it, but they will still, the first time, have to decide whether it's real.

This is why:

- **Docs age badly around wisdom.** The knowledge-part stays accurate as long as nothing breaks; the wisdom-part can't be written down densely enough to remain useful two engineers later.
- **Pairing is higher-bandwidth than writing.** Pairing transfers wisdom *by demonstration* — the junior watches the senior decide, and the decision-shape is transmitted. Writing transfers only the decision's rationale, not its shape.
- **Shadowing beats reading.** On-call shadowing is the wisdom-transfer ritual. It works not because the shadow learns the dashboards; they'd learn those faster by reading. It works because they learn the *rhythm* — what the senior notices, skips, escalates, delays.

## Hesse's rougher claim, checked

The stronger form — "any truth put into words is one-sided" — is stronger than necessary. Falsifiable claims *can* be put into words; mathematical theorems can. What Hesse is pointing at is that *lived* truths (how to be in grief, how to love, how to run a team through a bad quarter) resist verbal compression without loss. A good test: if the truth survives being restated by a stranger who never lived it, it was knowledge. If it requires the teller's history to land, it's wisdom.

## How to use this distinction

- **When writing.** Ask: am I transferring *knowledge* (facts, procedures, structures) or trying to transfer *wisdom* (felt judgment)? If the latter, add demonstrations, examples, and caveats rather than crisper rules. The reader will still have to re-earn it; your job is to reduce the tuition.
- **When teaching.** Don't front-load the wisdom part. Let the junior generate the bad decision. Then show them what you saw. The re-earning was the point; the debrief just shortens the distance.
- **When learning.** If you're reading a classic and it feels thin, it may be wisdom you haven't earned yet. Re-read later; the same sentence will be denser.
- **When making decisions.** Name what is knowledge and what is wisdom in the decision. "I know the latency numbers; I *suspect* the on-call is about to burn out" — the first is falsifiable with data, the second is the tacit claim you're making from pattern-matching. Both matter; pretending the second is the first degrades the decision.

## Related

- [[../books/siddhartha|Siddhartha]] — source
- [[../books/tuesdays-with-morrie|Tuesdays With Morrie]] — Morrie is Hesse's teacher-figure in modern dress
- [[../books/the-pilgrimage|The Pilgrimage]] — Coelho; wisdom as walked, not lectured
- [[three-sources-of-meaning|Three sources of meaning]] — Frankl: the "why" is wisdom; the theory of meaning is knowledge
- [[personal-legend|Personal Legend]] — Coelho; the vocation that cannot be prescribed
- [[hemispheric-attention|Hemispheric attention]] — McGilchrist; the right-mode is the wisdom-ingesting side
- [[flow-state|Flow state]] — the phenomenology of wisdom-in-action
- [[falsifiability|Falsifiability]] — the boundary of knowledge
