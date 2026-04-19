---
type: moc
domain: learning
status: live
created: 2026-04-19
updated: 2026-04-19
sources: []
---

# Learning — MOC

General knowledge from books, articles, podcasts, videos, papers. CS, management, philosophy, psychology, science (non-BMS).

Parent: [[../index|Wiki index]]

## Concepts

### Systems & reliability
- [[concepts/error-budget|Error budget]] — allowable unreliability; reframes SRE goal away from "zero outages"
- [[concepts/toil|Toil]] — manual, repetitive work that scales linearly with service growth
- [[concepts/golden-signals|Four golden signals]] — latency, traffic, errors, saturation
- [[concepts/use-method|USE method]] — utilization, saturation, errors per resource
- [[concepts/latency-vs-throughput|Latency vs throughput]] — why averages and unqualified "latency" lie
- [[concepts/scalability|Scalability]] — load-parameter-shaped architecture
- [[concepts/fault-vs-failure|Fault vs failure]] — faults are local; failures are what users see
- [[concepts/unix-filesystem-hierarchy|Unix filesystem hierarchy]] — FHS; the map SRE triage assumes
- [[concepts/unix-file-permissions|Unix file permissions]] — rwx, octal modes, the `=` gotcha
- [[concepts/falsifiability|Falsifiability]] — Hawking/Popper: the demarcation test for a claim

### Meaning, purpose, work
- [[concepts/flow-state|Flow state]] — conditions for sustained deep work
- [[concepts/three-sources-of-meaning|Three sources of meaning]] — Frankl: work, love, courage in suffering
- [[concepts/memento-mori|Memento mori]] — mortality as calibration tool, not threat
- [[concepts/agape|Agape]] — Greek love-as-will; Coelho's root of the wisdom trinity
- [[concepts/fighting-the-good-fight|Fighting the good fight]] — Coelho: the three symptoms of killing your dreams
- [[concepts/personal-legend|Personal Legend]] — Coelho: the vocation you're meant to pursue
- [[concepts/labyrinth-of-suffering|Labyrinth of suffering]] — Green: pain as a one-path winding, not a maze
- [[concepts/intrusive-thoughts-vs-self|Intrusive thoughts vs self]] — Green + Gilbert: CBT defusion
- [[concepts/wisdom-vs-knowledge|Wisdom vs knowledge]] — Hesse: what docs transfer vs what has to be re-earned
- [[concepts/karma-yoga|Karma yoga]] — Gita/Yogananda: full engagement, open-handed outcome
- [[concepts/samskaras|Samskaras]] — Yogananda + Walton: behavioural templates deepened by repetition
- [[concepts/quiet-desperation|Quiet desperation]] — Thoreau/Thomas: the chronic-self-betrayal diagnostic

### Leadership & influence
- [[concepts/golden-circle|Golden circle]] — Sinek: WHY → HOW → WHAT
- [[concepts/inspire-vs-manipulate|Inspire vs manipulate]] — the two ways to influence behavior
- [[concepts/social-vs-market-norms|Social vs market norms]] — Ariely: mixing them destroys the social norm
- [[concepts/customer-development|Customer development]] — Blank: startup = search, not execution

### Communication & relationships
- [[concepts/mr-fix-it-trap|Mr. Fix-It trap]] — Gray (de-gendered): solutions-as-invalidation; listen-vs-solve
- [[concepts/perspective-taking|Perspective-taking]] — Atticus's "climb into his skin"; epistemic prerequisite to judgment
- [[concepts/first-impression-signals|First-impression signals]] — Lowndes distilled; 4 load-bearing + 4 amplifiers
- [[concepts/mbti-perception-judgment|MBTI perception vs judgment]] — Myers's usable core minus the unreliable inventory
- [[concepts/hemispheric-attention|Hemispheric attention]] — McGilchrist: narrow/focussed vs broad/vigilant modes
- [[concepts/books-as-mirrors|Books as mirrors]] — Zafón: reading projects the reader; diverse reviewers catch more bugs

### Political & social
- [[concepts/bread-and-circuses|Bread and circuses]] — Juvenal/Collins: subsistence + spectacle for civic agency

### Ideas with asterisks
- [[concepts/law-of-attraction|Law of attraction]] — Byrne's "The Secret"; defensible cognitive mechanisms + mystical-physics overreach
- [[concepts/divine-proportion|Divine proportion (φ)]] — real in self-similar growth; oversold in art/body claims
- [[concepts/coincidence-vs-narrative|Coincidence vs narrative]] — Yoon + Zafón: story-generator vs null-tester; post-mortem epistemics

## Sub-areas

### Books

Compiled source-summaries:

**Systems & CS**
- [[books/site-reliability-engineering|Site Reliability Engineering]] (Murphy et al.) — Google SRE canon
- [[books/designing-data-intensive-applications|Designing Data-Intensive Applications]] (Kleppmann) — distributed-systems primer
- [[books/systems-performance|Systems Performance]] (Gregg) — USE method, Linux perf methodology
- [[books/system-design-interview|System Design Interview]] (Xu) — compact scaling checklist
- [[books/linux-for-beginners|Linux for Beginners]] (Cannon) — CLI, FHS, permissions primer
- [[books/a-brief-history-of-time|A Brief History of Time]] (Hawking) — falsifiability, anthropic principle, time as universe property

**Philosophy, meaning, mortality**
- [[books/ikigai|Ikigai]] — purpose + flow
- [[books/sophies-world|Sophie's World]] (Gaarder) — philosophy primer, pre-Socratics → Socrates
- [[books/mans-search-for-meaning|Man's Search for Meaning]] (Frankl) — meaning as the primary need
- [[books/tuesdays-with-morrie|Tuesdays With Morrie]] (Albom) — mortality-as-teacher memoir
- [[books/the-pilgrimage|The Pilgrimage]] (Coelho) — agape, fighting the good fight, Camino de Santiago
- [[books/the-alchemist|The Alchemist]] (Coelho) — Personal Legend, heart-listening
- [[books/eat-pray-love|Eat Pray Love]] (Gilbert) — pleasure as obligation; soul-mate-as-mirror
- [[books/siddhartha|Siddhartha]] (Hesse) — wisdom-can't-be-passed-on; river-as-eternal-present
- [[books/the-monk-who-sold-his-ferrari|The Monk Who Sold His Ferrari]] (Sharma) — self-help compression of material also in Hesse/Coelho
- [[books/yogananda-bhagavad-gita|Bhagavad Gita]] (Yogananda) — karma yoga, samskaras, the body-as-kingdom
- [[books/thomas-the-big-switch|The Big Switch]] (Thomas) — engineer career-change fable; quiet-desperation operationalised
- [[books/watt-mindfulness|A Practical Guide to Mindfulness]] (Watt) — short; the panning-camera scan
- [[books/and-every-morning-the-way-home|And Every Morning…]] (Backman) — dementia novella (placeholder)

**Leadership, influence, psychology**
- [[books/start-with-why|Start With Why]] (Sinek) — golden circle, leadership by purpose
- [[books/leaders-eat-last|Leaders Eat Last]] (Sinek) — circle of safety (placeholder)
- [[books/how-to-win-friends-and-influence-people|How to Win Friends and Influence People]] (Carnegie) — placeholder
- [[books/the-48-laws-of-power|The 48 Laws of Power]] (Greene) — Machiavellian power dynamics
- [[books/predictably-irrational|Predictably Irrational]] (Ariely) — behavioral economics
- [[books/the-secret|The Secret]] (Byrne) — law of attraction, with critique
- [[books/men-are-from-mars-women-are-from-venus|Men Are from Mars, Women Are from Venus]] (Gray) — Mr. Fix-It trap
- [[books/turtles-all-the-way-down|Turtles All the Way Down]] (Green) — OCD, intrusive-thoughts-vs-self
- [[books/looking-for-alaska|Looking For Alaska]] (Green) — labyrinth of suffering, forgiveness-as-survival
- [[books/how-to-talk-to-anyone|How to Talk to Anyone]] (Lowndes) — 90+ tactics → load-bearing four + four amplifiers
- [[books/gifts-differing|Gifts Differing]] (Myers-Myers) — MBTI framework; keep vocabulary, reject inventory
- [[books/the-master-and-his-emissary|The Master and His Emissary]] (McGilchrist) — hemispheric attention, mode-switching
- [[books/walton-emotional-intelligence|A Practical Guide to Emotional Intelligence]] (Walton) — thin; behavioural-templates kernel
- [[books/tuhovsky-communication-skills-training|Communication Skills Training]] (Tuhovsky) — placeholder

**Money, work, entrepreneurship**
- [[books/the-millionaire-fastlane|The Millionaire Fastlane]] (DeMarco) — wealth as process, the three roadmaps
- [[books/the-million-dollar-weekend|The Million Dollar Weekend]] — bias-to-action entrepreneurship playbook
- [[books/the-100-startup|The $100 Startup]] (Guillebeau) — micro-business manifesto (placeholder)
- [[books/the-four-steps-to-the-epiphany|The Four Steps to the Epiphany]] (Blank) — Customer Development
- [[books/the-gig-economy|The Gig Economy]] (Mulcahy) — ten-rule gig-era playbook

**Fiction**
- [[books/origin|Origin]] (Brown) — science vs religion, First Cause, the two questions
- [[books/the-da-vinci-code|The Da Vinci Code]] (Brown) — symbology, divine proportion, sacred feminine
- [[books/the-hunger-games|The Hunger Games]] (Collins) — silence as dissent
- [[books/catching-fire|Catching Fire]] (Collins) — interrogating one's own motive; facing the fight
- [[books/mockingjay|Mockingjay]] (Collins) — Panem et Circenses; Snow/Coin equivalence
- [[books/all-the-light-we-cannot-see|All the Light We Cannot See]] (Doerr) — radio as mass influence; history-by-victors
- [[books/to-kill-a-mockingbird|To Kill A Mockingbird]] (Lee) — perspective-taking; conscience over majority; real courage
- [[books/all-the-bright-places|All the Bright Places]] (Niven) — Waiting Place; "there is only now"; acceptance-of-loss
- [[books/animal-farm|Animal Farm]] (Orwell) — Squealer; the four-line slide from original vow to "more equal"
- [[books/yoon-the-sun-is-also-a-star|The Sun is also a Star]] (Yoon) — determinism vs fate; lust/attraction/attachment; Sagan's apple pie
- [[books/zafon-shadow-of-the-wind|The Shadow of the Wind]] (Zafón) — books-as-mirrors; prisons-of-words; post-war memory
- [[books/zusak-the-book-thief|The Book Thief]] (Zusak) — not-leaving as love; every pattern tips
- [[books/todd-after|After]] (Todd) — placeholder
- [[books/pride-and-prejudice|Pride and Prejudice]] (Austen) — placeholder
- [[books/thirteen-reasons-why|Thirteen Reasons Why]] (Asher) — placeholder
- [[books/and-then-there-were-none|And Then There Were None]] (Christie) — placeholder
- [[books/the-great-gatsby|The Great Gatsby]] (Fitzgerald) — placeholder
- [[books/eleanor-and-park|Eleanor & Park]] (Rowell) — placeholder

_(0 sources remain pending in `sources/learning/books/Kindle Highlights/`. All 63 Kindle highlight sources compiled. Next ingest runs will process `inbox/urls.md`, new source files, or `/ingest-file <path>` additions.)_

### Computer Science
_(empty — `archive/3. Resources/Computer Science/` 40+ files: algorithms, AI, AWS, system design, technologies)_

### Management
_(empty — `archive/3. Resources/Management/` 4 files; `archive/loose/Making of a Manager.md` is substantive)_

### Communication
_(empty — `archive/2. Areas/Communication/` 3 files: First Impressions, Think Fast Talk Smart, Someone likes you)_

### Philosophy
_(empty — `archive/3. Resources/Philosophy/` 3 files)_

### Concepts
_(empty — `archive/3. Resources/Intersting Concepts-Ideas/`)_

### Podcasts
_(empty — `archive/loose/` has 4 podcast notes; `archive/3. Resources/PodCast/Bella Vitta Podcast.md`)_

### Articles
_(empty — `archive/3. Resources/Articles/Body Language.md`, `archive/loose/EBS - Millions-of-tiny-databases.md`)_

### AI / ML
_(empty — `archive/3. Resources/Computer Science/Artificial Intelligence/`, `archive/loose/AI Workshop.md`)_

## Synthesis bridges
- [[../synthesis/sre-practice-for-bms|SRE practice for BMS]] — learning ↔ work
- [[../synthesis/linux-fundamentals-for-sre|Linux fundamentals for SRE]] — learning ↔ work; staircase from Cannon → Gregg → SRE canon
