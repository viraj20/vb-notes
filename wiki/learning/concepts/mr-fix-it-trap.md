---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Gray-Men Are from Mars, Women Are from Venus.md
---

# Mr. Fix-It trap

Parent: [[../index|Learning MOC]]

The communication failure mode where one party wants to be heard and the other, trying to help, offers solutions. The helper's impulse is genuine; the effect is invalidation. Named by Gray in [[../books/men-are-from-mars-women-are-from-venus|Men Are from Mars, Women Are from Venus]]; de-gendered here.

## The pattern (Gray, loc 291, 296, 386)

> "When a woman innocently shares upset feelings or explores out loud the problems of her day, a man mistakenly assumes she is looking for some expert advice. He puts on his Mr. Fix-It hat and begins giving advice… He has no idea that by just listening with empathy and interest he can be supportive."

Stripped of Gray's gendering, the pattern is:

1. **A** shares a frustration — venting, processing out loud, seeking acknowledgement.
2. **B** hears a problem statement and responds with solutions.
3. **A** feels unheard; the solutions, however good, arrive as "your problem is trivial, here is how to fix it."
4. Both parties end frustrated: B tried to help and got rebuffed; A tried to be heard and got diagnosed.

## Why solutions feel like invalidation

Solutions presuppose a diagnosis. When A hasn't finished articulating the problem, a solution implicitly tells them: (a) the problem is smaller than they think, (b) they should have solved it themselves, or (c) they're being inefficient by talking about it instead of fixing it. Even when none of those were intended, all three land.

## The inverse: unsolicited advice trap (loc 283, 328)

Symmetric failure mode: the "helper" sees something the other person could do better and offers advice without being asked. Effect (Gray, loc 283): "to presume that he doesn't know what to do or that he can't do it on his own." Advice lands as diagnosis of incompetence.

## The fix, compressed

Before responding, ask one of:

- **"Do you want me to listen, or do you want ideas?"**
- **"Are you venting or are you problem-solving?"**

If listening: acknowledge the frustration, reflect the content, ask what they need. If problem-solving: then offer solutions.

Cheap, reliable, works across any relationship. The explicitness is a feature, not a clumsy workaround — it externalises a mode-switch that is otherwise mis-inferred.

## Where this applies in engineering work

- **1:1s with reports.** The single most common listening-vs-solving failure in tech management. "My sprint is hell" is usually not a feature request.
- **Incident post-mortems.** When someone is walking through what went wrong, interrupting with "well, you should have…" produces the Mr. Fix-It trap at team scale. Let the narrative finish first.
- **Code review.** Asking "what tradeoffs did you consider?" lands differently than "you should have used X" — even when the review content is identical.
- **On-call handoff.** Outgoing engineer venting about an ugly incident doesn't need debugging advice; they need acknowledgement that it was ugly.

## Related

- [[../books/men-are-from-mars-women-are-from-venus|Men Are from Mars, Women Are from Venus]] — source (gendered framing)
- [[../books/how-to-win-friends-and-influence-people|How to Win Friends and Influence People]] — Carnegie's listen-more heuristic
- [[../books/start-with-why|Start With Why]] — Sinek's framing of WHY-before-WHAT
- [[social-vs-market-norms|Social vs market norms]] — Ariely: advice can be a market-norm response to a social-norm moment
- [[inspire-vs-manipulate|Inspire vs manipulate]] — Sinek; the same "help vs. impose" axis
