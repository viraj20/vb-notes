---
type: source-summary
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Yoon-The Sun is also a Star.md
---

# The Sun is also a Star — Nicola Yoon

Parent: [[../index|Learning MOC]]

A 12-hour New York City love story between Natasha (Jamaican, about to be deported) and Daniel (Korean-American, conflicted about his parents' path for him). What makes this book wiki-worthy isn't the romance; it's the *frame* Yoon uses to sit next to the romance — a running debate between **determinism** ("life is just a series of dumb decisions and indecisions and coincidences we ascribe meaning to," loc 2085) and **fate** ("love and dark matter were the same—the only thing that kept the universe from flying apart," loc 3551).

The book is structured as a love story but reads as an extended meditation on the question: *when we retrospectively narrate our lives as meaningful, are we discovering the meaning or making it up?*

## The four load-bearing ideas

### 1. The three phases of love (scientific literature Natasha cites)

Loc 1139:

> "lust, attraction, and attachment."

A standard textbook decomposition (Fisher et al.) — Natasha uses it to defend a position that romantic love is "temporary and nonprovable" (loc 837). The decomposition is correct; her conclusion is not — attachment is the stable phase and is *provable* (neurochemical correlates, oxytocin), it just runs on a longer timescale than the book's 12 hours.

Why it matters for the wiki: the three-phase taxonomy is the most useful thing in romance-writing that isn't in [[eat-pray-love|Gilbert]] or [[men-are-from-mars-women-are-from-venus|Gray]]. Keep it.

### 2. The koi no yokan distinction

Loc 824:

> "There's a Japanese phrase that I like: koi no yokan. It doesn't mean love at first sight. It's closer to love at second sight. It's the feeling when you meet someone that you're going to fall in love with them. Maybe you don't love them right away, but it's inevitable that you will."

A more honest version of "love at first sight." The claim isn't that you love them now — it's that your prediction-engine has returned a high-confidence forecast. Whether the forecast is reliable is a separate question (frequently no, sometimes yes). But the feeling is distinct from lust-at-first-sight and worth naming.

### 3. Coincidence vs fate — the book's running argument

Three Natasha-side claims:

- "Life is just a series of dumb decisions and indecisions and coincidences that we choose to ascribe meaning to." (loc 2085)
- "We tell ourselves there are reasons for the things that happen, but we're just telling ourselves stories. We make them up. They don't mean anything." (loc 2092)
- "A series of small coincidences that we say means everything because we want to believe that our tiny lives matter on a galactic scale." (loc 2128)

And Daniel's side:

- "You know the way we feel right now? This connection between us that we don't understand and we don't want to let go of? That's God." (loc 2819)

The book doesn't resolve which is right. It treats the question as genuine. See [[../concepts/coincidence-vs-narrative|coincidence vs narrative]] for the concept — the engineering analogue is post-incident narrative smoothing (did this outage happen *because* of the deploy, or because of five unrelated things that coincidentally stacked?).

### 4. Sagan's apple pie — everything depends on everything

Loc 64, 71:

> "CARL SAGAN SAID that if you want to make an apple pie from scratch, you must first invent the universe."

> "To make a thing as simple as an apple pie, you have to create the whole wide world."

A dependency-graph argument. Every "simple" thing rests on a stack of non-simple things. Engineering analogue: "it's just a cache invalidation" → depends on the cache; depends on what you're caching; depends on the DB that's the cache's source; depends on the network between them; depends on the deploy that changed any of those. Never *just* anything.

## What to skip

- **Donald's "all futures destroyed in a single moment" riff** (loc 700) — true but generic. [[mans-search-for-meaning|Frankl]] handles this more rigorously.
- **"Hearts don't break, they just stop working"** (loc 3165) — memorable poetry; not a claim.
- **Fish-on-a-hook metaphor** (loc 2284) — one of several "obsessive thought" depictions, better in [[turtles-all-the-way-down|Green]].
- **The "eyes are windows to the soul"** (loc 2897) — folk; see [[how-to-talk-to-anyone|Lowndes]] for actual eye-signal tactics.

## Other notable passages

**Deportation stakes and citizenship irony.** The book's urgency comes from Natasha's 12-hour clock; Yoon keeps the political subtext close to the surface without sermonising. The opening frame — "Every moment in our lives has bought us to this single moment. A million futures lie before us. Which one will come true?" (loc 57) — is the deportation thesis in disguise. Natasha's observation that "people who were actually born here had to prove they were worthy enough to live in America, this would be a much less populated country" (loc 1231) is the book's sharpest political line. Dreams are the collateral: "dreams never die even when they're dead" (loc 2217).

**Relationship-building as protocol.** Yoon plants two concrete, executable tactics inside the romance. Daniel's use of the Aron 36-questions protocol (loc 934) — the same one published in "To Fall in Love With Anyone, Do This" — is a rare moment of an intimacy-procedure appearing in fiction rather than a self-help book. The counter-tactic sits later: "IT'S HARD TO love someone who doesn't love you back" (loc 1630) — a rule about when to stop running the procedure at all.

**Falling vs choosing.** Yoon worries the agency question from several angles. "The thing about falling is you don't have any control on your way down" (loc 2029) is the passive frame; "love always changes everything" (loc 3125) is the fait-accompli frame; "No one needs to get bruised up falling in love" (loc 1424) pushes back against both by insisting the fall can be deliberate. The synthesis lands at loc 1608: "Maybe part of falling in love with someone else is also falling in love with yourself" — reframing the whole question as self-directed rather than other-directed.

**Identity as inheritance.** Two lines do quiet work on the "am I my parents" question that powers Daniel's subplot. On names: "Names are powerful things. They act as an identity marker and a kind of map, locating you in time and geography" (loc 206). On fathers: "'You're not your dad,' I say, but he doesn't believe me. I understand his fear. Who are we if not a product of our parents and their histories?" (loc 1562). Daniel's raison d'être (loc 1508) and his suit-as-costume moment (loc 396) are both expressions of the same anxiety: the cost of performing a role chosen for you.

**Natasha's defensive empiricism.** The book's most interesting characterisation move is that Natasha's anti-romance stance is itself a passion. Daniel names it twice: "I wonder if she realizes how passionate she is about not being passionate" (loc 1102) and "wonder why a girl who is so obviously passionate is so adamantly against passion" (loc 1712). The underlying worldview comes earlier — "how can you trust something that can end as suddenly as it begins?" (loc 654), love as a decaying isotope (loc 662), the flat assertion that "No one wants to believe that life is random" (loc 411) against the softer acknowledgement that "almost everyone believes that there's some meaning, some willfulness to life" (loc 409). Her epistemology is defensible; the book's argument is that defensible is not the same as correct.

**Aphorisms worth keeping.** A handful of lines travel well outside the novel. "To grow up is to grow apart" (loc 1411) is the cleanest statement of the book's secondary theme. "Some people exist in your life to make it better. Some people exist to make it worse" (loc 2651) is unusable as advice but accurate as taxonomy. "Almost everything in the night sky gives off light. Even if we can't see it, the light is still there" (loc 3523) closes the Sagan-apple-pie loop — the invisible stack is still a stack. "Fate has a Reason and, though you may not know it, there's a certain comfort in knowing that there's a Plan" (loc 2108) and "You should never take long shots... if the long shot is your only shot, then you have to take it" (loc 423) are the book's cleanest statements of the fate-vs-odds tension. The closing note, "love changes all things all the time. That's what love is for" (loc 3508), is the only place Yoon lets narrative win outright.

## The book's honest contribution

Yoon does something unusual for a YA romance: she lets both Natasha (empiricist, anti-fate) and Daniel (narrative-meaning, pro-fate) be intelligently defended. The book's answer is neither; it's that *the meaning we make is real and also made-up simultaneously* — the same coincidence both is a statistical accident and is, after the fact, the reason two people's lives changed. The falsifiable and the felt coexist. See [[../concepts/falsifiability|falsifiability]] for the boundary.

## For engineering contexts

### Post-mortem narrative vs coincidence

The running debate maps directly onto how RCAs are written. If five events coincided to produce the outage, did they happen *because of* the deploy (narrative), or did five independent things happen to coincide that day (statistics)? Honest RCAs resist the narrative smoothing. See [[../concepts/coincidence-vs-narrative|coincidence vs narrative]] and [[animal-farm|Orwell]]'s Squealer problem.

### Sagan's apple pie and system scope

"Invent the universe" is the estimator's trap — every feature depends on the full system, and naive scope estimates under-count. Gregg's [[systems-performance|USE method]] is partly a defense: at least check the universe you're resting on.

## Related

- [[../concepts/coincidence-vs-narrative|Coincidence vs narrative]] — extracted concept
- [[../concepts/falsifiability|Falsifiability]] — where the Natasha/Daniel debate touches ground
- [[eat-pray-love|Eat Pray Love]] — Gilbert; the next-phase romance
- [[men-are-from-mars-women-are-from-venus|Men Are from Mars, Women Are from Venus]] — Gray; communication adjunct
- [[animal-farm|Animal Farm]] — Orwell; narrative-smoothing parallel
- [[turtles-all-the-way-down|Turtles All the Way Down]] — Green; obsessive thought
- [[all-the-bright-places|All the Bright Places]] — Niven; YA romance with depression overlay
- [[systems-performance|Systems Performance]] — Gregg; the apple-pie defense
