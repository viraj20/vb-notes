---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Yogananda-God Talks with Arjuna The Bhagavad Gita.md
  - sources/learning/books/Kindle Highlights/Walton-A Practical Guide to Emotional Intelligence.md
---

# Samskaras (behavioural templates)

Parent: [[../index|Learning MOC]]

Yogananda ([[../books/yogananda-bhagavad-gita|Bhagavad Gita]], loc 1838):

> "A thought or physical act once performed does not cease to be, but remains in the consciousness in a more subtle or 'melted' form as an impression of that gross expression of thought or action. These impressions are called samskaras."

[[../books/walton-emotional-intelligence|Walton]], loc 167, same mechanism in Western-psychology register:

> "building up behavioural templates, which are stored in your brain and used for…"

The claim shared: every repeated thought or action leaves a trace that shapes the probability of the same thought or action arising next time. The mechanism is well-supported in the cognitive-neuroscience literature (Hebbian learning, habit formation, basal-ganglia consolidation) — the Gita and the EI-book are two different vocabularies for the same thing.

## Why the concept is load-bearing

The move that samskaras names is the thing habits actually do, minus the "habit = conscious choice" confusion. A samskara:

- **Fires without deliberation** once set.
- **Deepens with each firing** — the track gets a little more worn.
- **Is agnostic to whether the behaviour is adaptive.** "Always check Slack first thing in the morning" is a samskara; so is "always doom-scroll when anxious"; so is "always ask the customer what they're trying to accomplish before offering solutions."

The Gita's framing makes a claim Western habit-research usually doesn't: samskaras carry across lifetimes. De-sectarianise: even without reincarnation, the claim *within* a lifetime is strong — your 40-year-old nervous system is carrying templates you set down at 8 and haven't examined since.

## The three practical questions

Given samskaras exist, the useful questions are:

1. **Which of my current automaticities are samskaras I chose, and which did I set down without noticing?** Most are the latter.
2. **Which samskaras are currently shaping decisions I think I'm making fresh?** E.g., the "always say yes to the senior eng's ask" template from an early job shapes present-day overcommitment.
3. **What new samskaras am I writing right now?** Every repeated action under emotional context is a deposit into the template system. On-call over a year sets down templates that will fire for the next ten.

## Engineering applications

### On-call builds samskaras you can't easily choose

The first three months on-call, you think about every alert. By month six, you've built templates: "this alert always means X; skip to the check for X." The templates are efficient — they're the reason senior oncalls are faster. They're also dangerous: the template fires whether or not *this specific alert* is actually X this time. See [[falsifiability|falsifiability]] — the discipline of naming "what would falsify this template's prediction" fights samskara-drift.

The bad samskaras on-call builds:

- "Acknowledge and wait" for alerts you've seen flap before — rights until the day the flap is real.
- "Escalate immediately to the team that usually owns this" — rights until the day the ownership silently changed.
- "Silence it and fix it in the morning" — rights until the morning is too late.

The discipline is periodic template-audit: which of my on-call reflexes are still correct?

### Code review builds evaluative samskaras

After 500 PRs, you develop a reflex read for "this function shape will have a bug." That reflex is a samskara. It's usually correct. It's also why senior reviewers sometimes miss novel bug classes — the template didn't include them, and the template fires faster than the novel-bug detector.

### Unchecked toil writes the wrong samskara

Every time you paper over a bad alert instead of fixing it, the "paper over" template sets deeper. Three months in, the skip-the-fix reflex fires automatically. [[toil|Toil]] is not just work-that-scales; it's work that builds bad samskaras if left unchecked. The SRE move — "if you touched this alert twice, file a ticket to fix the root cause" — is samskara-hygiene, not just process.

### Morning rituals are samskara-deposit decisions

Which of your first-20-minutes-of-the-day behaviours are you choosing, and which are templates from a prior job/life that fire without examination? The first-20-minutes set the neurochemical floor for the day — these are the highest-leverage samskaras to audit.

## Relation to adjacent concepts

- [[karma-yoga|Karma yoga]] — the Gita's companion concept. Karma-yoga is the *attitude* discipline that produces the right samskaras regardless of outcome.
- [[intrusive-thoughts-vs-self|Intrusive thoughts vs self]] — CBT defusion works against unwanted-thought samskaras. The defusion itself, practiced, becomes a healthier samskara.
- [[flow-state|Flow state]] — repeated flow deposits skill-related samskaras (the thing training a deliberate skill actually is).
- [[wisdom-vs-knowledge|Wisdom vs knowledge]] — wisdom is the sum of useful samskaras earned through experience. It cannot be transferred directly precisely because samskaras must be laid down by the person whose nervous system carries them.
- [[toil|Toil]] — toil builds the wrong samskaras.
- [[golden-signals|Four golden signals]] — the discipline of checking these regularly deposits the right observational samskaras.

## How to change a samskara

You don't overwrite a samskara; you outcompete it. The new behaviour, repeated under similar conditions, writes a stronger parallel track. Over weeks-to-months the new track fires first. Old track doesn't vanish; it's just not the default. This is why habit change is slow and why willpower-at-the-moment rarely works — you're trying to beat a deeply-grooved track with a single firing.

## Related

- [[../books/yogananda-bhagavad-gita|Bhagavad Gita]] — source (Yogananda)
- [[../books/walton-emotional-intelligence|Walton EI]] — Western-register source
- [[karma-yoga|Karma yoga]] — companion discipline
- [[flow-state|Flow state]] — the skill-samskara engine
- [[toil|Toil]] — the bad-samskara hazard
- [[wisdom-vs-knowledge|Wisdom vs knowledge]] — wisdom as sum of earned samskaras
- [[intrusive-thoughts-vs-self|Intrusive thoughts vs self]] — defusion as samskara-hygiene
- [[falsifiability|Falsifiability]] — the audit discipline against template-drift
- [[golden-signals|Four golden signals]] — deliberate observational samskara
- [[../books/siddhartha|Siddhartha]] — Hesse; adjacent vocabulary
