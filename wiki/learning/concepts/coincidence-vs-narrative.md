---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Yoon-The Sun is also a Star.md
  - sources/learning/books/Kindle Highlights/Zafon-The Shadow Of The Wind.md
---

# Coincidence vs narrative

Parent: [[../index|Learning MOC]]

The question [[../books/yoon-the-sun-is-also-a-star|Yoon]] sits with for 300 pages and [[../books/zafon-shadow-of-the-wind|Zafón]] sits with for 500: when events in our lives line up, are we *discovering* meaning or *constructing* it?

Natasha (Yoon, loc 2085):

> "Life is just a series of dumb decisions and indecisions and coincidences that we choose to ascribe meaning to."

Zafón (loc 7391), the other side:

> "coincidences are the scars of fate. There are no coincidences, Daniel. We are puppets of our subconscious desires."

Both framings are under-specified. The useful concept sits between them: **we are narrative-making machines running on a reality that includes random coincidence; honest thinking requires distinguishing which is operating when.**

## The three regimes

Any given set of aligned events is in one of three regimes:

1. **Pure coincidence.** The events happened to co-occur for no reason other than sample space. If you flip a coin 1000 times, long runs happen — their occurrence is not evidence of a biased coin. Narrative-making machine will generate an explanation anyway.
2. **Common cause.** The events co-occur because a third factor drove both. The deploy *and* the latency spike both happened at 14:00 because someone pushed to prod at 14:00 — the deploy didn't cause the latency; a third event (prod push) caused both.
3. **Causal link.** Event A caused event B. This is the regime narrative-making assumes by default.

The epistemic failure mode: treating regime 1 or regime 2 events as regime 3. The opposite failure (treating regime 3 events as regime 1) is rarer but real — the sober-minded engineer who dismisses "the deploy caused the outage" as coincidence when it really didn't.

## The two adversaries

- **The storyteller.** In the absence of a story, the mind builds one. After-the-fact rationalisation is *automatic*; it is not a chosen act. When Daniel meets Natasha the day her family is being deported, the story-generator in both of them produces "we met for a reason" before either has consciously considered it.
- **The null-tester.** Good thinking includes an active discipline to ask "would these events have looked the same if nothing were causally connecting them?" Most day-to-day thinking doesn't deploy this, because it's expensive.

See [[falsifiability|falsifiability]]. The Popperian move — "what would falsify this claim?" — is exactly the null-tester's discipline, applied to the story-generator's output.

## For engineering contexts

### Post-incident narrative smoothing

The most dangerous deployment of this bug is post-incident analysis. The graph shows:

- 14:00 — deploy landed
- 14:02 — latency spike begins
- 14:04 — SEV-2 declared

The story-generator says: "the deploy caused it." The honest question is: *would 14:02's latency spike have looked the same if the deploy hadn't happened?*

Possibilities to rule out before the RCA goes final:

- **Coincidence.** The latency spike was caused by an external traffic pattern or a downstream dependency degradation that was independent. The deploy is a red herring. Check same-time-of-day from the previous week.
- **Common cause.** Something upstream of both (a runbook execution, an internal migration, a config push) caused both the deploy-release-pipeline to fire *and* an independent latency degradation. Check the surrounding ops timeline.
- **Causal, direct.** The deploy did it.
- **Causal, indirect.** The deploy didn't cause the latency directly, but increased load on a subsystem that was already near a tipping point.

Writing the RCA as if the first bullet is impossible is narrative smoothing. [[../books/animal-farm|Orwell]]'s Squealer moves in here: the story that "the deploy caused the outage" becomes the *official* story, and future decisions (more gated deploys, more process) are made against a story that might not be true.

### Hiring stories

Every hire's onboarding week contains a minor outage. The story-generator says "the new hire caused it" because the correlation is salient. Possibility space: the outage would have happened anyway; the hire was the first person to touch a broken system that was waiting to fail; or, yes, the hire caused it. Treating the third as the default hurts both the hire and the org's ability to find real root causes.

### Team performance

Q3 was bad. The story-generator says "the bad hire in July caused it" or "the re-org in August caused it." It might be either; it might be a set of unrelated factors (market conditions, a specific customer loss, a platform regression). The narrative-smoothed version produces the wrong fix (fire the July hire, reverse the August re-org) when the real fix is elsewhere.

## When to *trust* the narrative

The discipline isn't to treat all narratives as false. Sometimes the story-generator is right — our pattern-recognition is cheap and often accurate.

Trust the narrative when:

- **The same pattern repeats across independent instances.** Once is coincidence; seven times is a pattern.
- **You can propose a mechanism that predicts new instances.** Not just post-hoc fit.
- **Removing the putative cause changes the effect.** A/B test, rollback, controlled intervention.

Distrust the narrative when:

- **It's a single salient co-occurrence.**
- **It has strong emotional content.** (Your story-generator is especially eager to find meaning in events that felt meaningful; this is exactly where it lies to you most.)
- **It provides no prediction for the next case.**

## The synthesis position

Natasha and Daniel, by the end of the book, are not argued out of their positions; they just hold them more lightly. Yoon's move is honest: you can believe "life is mostly random" *and* "what happened today between us was meaningful to me." The first is epistemics; the second is phenomenology. Holding them simultaneously without conflating them is the mature position.

Engineering translation: the outage happened for a reason (probably) *and* the specific story we tell about it will always be partial and somewhat narrative-shaped. Doing the best RCA you can doesn't mean the RCA captures objective truth; it means you've done the honest work to rule out the salient alternatives.

## Related

- [[../books/yoon-the-sun-is-also-a-star|The Sun is also a Star]] — source
- [[../books/zafon-shadow-of-the-wind|Shadow of the Wind]] — source
- [[../books/animal-farm|Animal Farm]] — Orwell; Squealer / narrative-smoothing
- [[falsifiability|Falsifiability]] — the null-tester's discipline
- [[perspective-taking|Perspective-taking]] — epistemic prerequisite to honest narrative
- [[wisdom-vs-knowledge|Wisdom vs knowledge]] — distinguishing the two is wisdom
- [[hemispheric-attention|Hemispheric attention]] — story-generator is left-mode; null-tester is a deliberate left-mode discipline against itself
- [[predictably-irrational|Predictably Irrational]] — Ariely; the irrational-but-predictable base case
- [[the-48-laws-of-power|The 48 Laws of Power]] — Greene; narrative construction as deliberate act
