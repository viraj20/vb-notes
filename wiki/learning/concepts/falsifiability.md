---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Hawking-A Brief History Of Time.md
---

# Falsifiability

Parent: [[../index|Learning MOC]]

Popper's criterion, restated by [[../books/a-brief-history-of-time|Hawking]] (loc 198, 207): a claim earns scientific standing by specifying, in advance, what observation would disprove it. Claims that cannot in principle be disproved are not wrong — they are not *the right shape to be either right or wrong*.

## Hawking's two-line definition

> "A theory is a good theory if it satisfies two requirements. It must accurately describe a large class of observations on the basis of a model that contains only a few arbitrary elements, and it must make definite predictions about the results of future observations."

> "A good theory is characterized by the fact that it makes a number of predictions that could in principle be disproved or falsified by observation."

Two constraints in tension: wide applicability *and* precise disprovable prediction. The tension is the point — a theory that covers everything vaguely fails on the second; one that predicts one specific thing fails on the first.

## Failure modes of non-falsifiable claims

1. **Unspecified predictions.** "Our platform is reliable." Over what window, at what percentile, under what load? Without numbers, the claim never fails.
2. **Retrodiction-only.** "This design handles every case we've seen." The design may be shaped around the cases; the test is what it predicts for cases you *haven't* seen.
3. **Motte-and-bailey rescues.** When a specific prediction fails, the claim retreats to a vaguer version ("well, *usually* it's reliable") that doesn't fail. The failed prediction never updates the underlying belief.
4. **Always-confirming frames.** [[law-of-attraction|Byrne's law of attraction]] is the canonical example — when manifestation "works" it's the law at work; when it doesn't, you lacked alignment. Nothing disproves it.

## In engineering

### SLOs as falsifiability contract

Service Level Objectives are the falsifiability move applied to reliability. "Reliable" is un-falsifiable. "99.9% of requests return within 200ms over a 30-day window" is falsifiable — at the end of the month, you either met it or you didn't. The [[error-budget|error-budget]] concept extends this: the SLO is a concrete prediction, and violating it has consequences rather than euphemistic re-framing.

### Post-mortem hypotheses

A root cause claim should pass Hawking's bar: what observation, if we made it, would show the root cause was actually something else? "The redis cache coherency bug caused the outage" is testable (recreate the cache state, verify the failure mode). "Technical debt caused the outage" is not.

### Architecture bets

When a design document claims "this will scale to 10× current load," the falsifiability question is: at what point would we know it didn't? A falsifiable bet specifies a test; an un-falsifiable one specifies only an aspiration.

### Product PRD predictions

"Users will love this" fails the test. "In an A/B test, feature X produces a statistically significant lift in 28-day retention" passes it.

## The limits of the concept

Falsifiability is load-bearing in physics; it is *partly* load-bearing everywhere else. Three caveats:

- **Not everything worth claiming is falsifiable.** Ethical claims, aesthetic judgments, some historical explanations. Falsifiability is a criterion for *scientific* claims, not for "useful" claims in general. Don't dismiss non-falsifiable claims as worthless.
- **Degrees, not binary.** Claims are more or less falsifiable. A precise numerical prediction is more falsifiable than a directional one, but the directional one is not nothing.
- **Auxiliary-hypothesis rescue.** In practice, a falsified prediction rarely kills a theory cleanly — people adjust the auxiliaries. Duhem-Quine. The spirit of falsifiability is about *willingness to update*, not about mechanical verdicts.

## How to apply in practice

Before publishing a claim (design doc, RCA, strategy memo), write one sentence: **"This claim would be wrong if we observed ___."** If you can't finish that sentence, the claim is not yet the right shape. Fix it or mark it as speculation.

## Related

- [[../books/a-brief-history-of-time|A Brief History Of Time]] — source
- [[error-budget|Error budget]] — the applied form in SRE
- [[law-of-attraction|Law of attraction]] — the un-falsifiable counter-example
- [[../books/the-secret|The Secret]] — source of that counter-example
- [[customer-development|Customer development]] — Blank: startup = search for falsifiable problem/solution fit
- [[fault-vs-failure|Fault vs failure]] — SRE's structural distinction; both concepts are falsifiable
- [[divine-proportion|Divine proportion]] — another page where I separated defensible claims from un-falsifiable overreach
