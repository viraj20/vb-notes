---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Lee-To Kill A Mockingbird.md
  - sources/learning/books/Kindle Highlights/Gray-Men Are from Mars, Women Are from Venus.md
---

# Perspective-taking

Parent: [[../index|Learning MOC]]

Atticus Finch's instruction to Scout ([[../books/to-kill-a-mockingbird|To Kill A Mockingbird]], loc 507):

> "You never really understand a person until you consider things from his point of view — until you climb into his skin and walk around in it."

The move is simple to name and hard to do: temporarily adopt the counterparty's information, constraints, incentives, and emotional state. Not sympathy (feeling with). Not projection (imagining what *you* would feel in their position). *Their* constraints, *their* information, *their* state.

## Why it's load-bearing

The default failure mode in any interaction is *modelling the other person as a worse version of yourself*. "Why would they do that? I wouldn't." Perspective-taking is the discipline of ruling that out before drawing conclusions.

Concrete form: before responding to a puzzling decision, force yourself to generate a reasonable story in which the decision was correct given what the decision-maker knew. If you can, you've done perspective-taking. If you can't, *you* are missing information, not them.

## Relation to adjacent concepts

- **[[mr-fix-it-trap|Mr. Fix-It trap]]** (Gray) — the operational version. Asking "do you want me to listen, or do you want ideas?" is perspective-taking compressed into a sentence. You're conceding that *their* frame determines the right response, not yours.
- **Carnegie's "talk about what the other person is interested in"** ([[../books/how-to-win-friends-and-influence-people|How to Win Friends]]) — perspective-taking applied to conversation topics. Atticus's Scout quote (loc 2693) names it the same way: "talk to people about what they were interested in, not about what you were interested in."
- **[[hemispheric-attention|Hemispheric attention]]** — perspective-taking is a right-mode capability; left-mode's tendency to categorize ("they're wrong because…") skips it.
- **[[three-sources-of-meaning|Frankl's response-choice]]** — at a deeper scale; choosing how to respond to what happens requires perspective-taking on the *situation* and on yourself.

## Failure modes

1. **Perspective-projecting, not perspective-taking.** "What would I do in their position?" is the wrong question. They are not you. The correct question is: "Given what *they* know and value, what makes their action reasonable?"
2. **Sympathy substituted for understanding.** Feeling bad for them does not equal understanding their decision. Perspective-taking is a cognitive act, not an emotional one.
3. **One-pass optimism.** Taking perspective once and then stopping. In conflict, you need to iterate — their reaction to your response updates your model of them.
4. **Weaponised perspective-taking.** Using the skill to manipulate — the dark side that [[inspire-vs-manipulate|Sinek]] warns about. The tool is neutral; application separates [[inspire-vs-manipulate|inspire from manipulate]].

## Atticus's stronger claim

Lee is making a claim beyond Carnegie's. Carnegie says: *use* perspective-taking to be more persuasive. Atticus says: *before* judging, you don't know enough. Perspective-taking isn't a persuasion technique — it's an epistemic prerequisite.

The engineering version: before a blameless post-mortem, you don't understand what happened. You understand what it *looked like it said* in the logs. Climbing into the on-call engineer's skin at 3 AM with bad observability is the prerequisite to writing the RCA honestly.

## For engineering contexts

- **Blameless post-mortems.** "Given what the on-call knew at 03:47, what would a competent engineer have done?" If the answer is "this," the RCA should say so. If the answer is "something better," locate the information gap, not the person.
- **Code review.** Before commenting "why did you do it this way," try: "What constraint produced this shape?" Often the answer is a constraint you didn't see. Sometimes it is genuine unfamiliarity — in which case, say so kindly.
- **Cross-team escalation.** Before escalating, model the counterparty team's current incentives and workload. Sometimes the action you want is cheap for you and expensive for them; the escalation should account for that.
- **1:1s with reports.** Their sprint is hell from *their* position. Your job is not to evaluate whether it's *objectively* hell; it's to understand what hell looks like from where they stand.
- **Customer development** ([[customer-development|Blank]]). The entire "search" mode of a startup is perspective-taking scaled up. You're modelling customers' constraints and information so precisely that you can predict what they'll say yes to.

## How to train it

- **Steel-man the decision you disagree with.** Write the best possible version of the argument on the other side. Required move before disagreeing in writing.
- **Before responding, restate.** In conversation, "So what you're saying is ___ — is that right?" surfaces your model for correction.
- **Assume context you don't have.** "They probably had a reason" is the right default when the person is competent. Perspective-taking tells you how to *look for* that reason rather than inventing one.

## Related

- [[../books/to-kill-a-mockingbird|To Kill A Mockingbird]] — source
- [[mr-fix-it-trap|Mr. Fix-It trap]] — Gray; operational form
- [[../books/how-to-win-friends-and-influence-people|How to Win Friends and Influence People]] — Carnegie
- [[../books/men-are-from-mars-women-are-from-venus|Men Are from Mars, Women Are from Venus]] — Gray; where the Mr. Fix-It concept lives
- [[hemispheric-attention|Hemispheric attention]] — right-mode capability
- [[three-sources-of-meaning|Three sources of meaning]] — Frankl
- [[customer-development|Customer development]] — Blank; scaled form
- [[inspire-vs-manipulate|Inspire vs manipulate]] — ethical calibration
- [[social-vs-market-norms|Social vs market norms]] — Ariely; what perspective-taking is for
