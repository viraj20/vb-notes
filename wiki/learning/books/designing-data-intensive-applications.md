---
type: source-summary
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md
---

# Designing Data-Intensive Applications (Kleppmann)

- Author: Martin Kleppmann
- ASIN: B06XPJML5D
- Source: Kindle highlights (44 annotations, early chapters)

Parent: [[../index|Learning MOC]] · Related: [[site-reliability-engineering|SRE book]] · [[systems-performance|Systems Performance]]

## Core argument

Data-intensive systems succeed on three axes — reliability, scalability, maintainability — and each demands different engineering trade-offs. The boundaries between relational, document, and graph models are blurring; pick for the load parameters that actually matter.

## Key ideas extracted

- **Fault vs failure** — a fault is a component deviating from spec; a failure is when the system stops serving the user. You can't drive faults to zero, so design fault-tolerance instead (loc 294). Anchors [[../concepts/fault-vs-failure|Fault vs failure]].
- **[[../concepts/scalability|Scalability]] is load-parameter-specific** — "architecture that scales well is built around assumptions of which operations are common and which are rare" (loc 626).
- **Read-vs-write trade-offs** — Twitter moved to fan-out-on-write because publish rate is two orders of magnitude below timeline-read rate (loc 464).
- **Tail latency amplification** — slow 99.9th-percentile requests often belong to the most valuable customers (most data) (loc 537, 573).
- **Shared-nothing** — distributing load across machines; the common wisdom was "scale up until you can't" (loc 605, 615).
- **Three maintainability properties** — operability, simplicity, evolvability (loc 644).
- **Accidental complexity** — complexity "not inherent in the problem" but from implementation; symptoms: state-space explosion, tight coupling, tangled deps, inconsistent naming (loc 685, 696).
- **Good software needs good ops** — "good operations can work around bad software; good software cannot run reliably with bad operations" (loc 654).
- **Schema-on-read vs schema-on-write** — document vs relational model trade-off; many-to-many relationships favor relational (loc 1187, 1205–1206).
- **Indexes** — speed reads, slow writes. "every index slows down writes" (loc 2405).

## Concepts this book anchors

- [[../concepts/scalability|Scalability]]
- [[../concepts/fault-vs-failure|Fault vs failure]]
- Tail latency — see [[../concepts/golden-signals|Golden signals]] and Gregg on percentiles

## Other notable passages

**Reliability framing and environmental drift.** Kleppmann defines reliability operationally as "continuing to work correctly, even when things go wrong" (loc 284), then localizes most outages to environmental assumptions that silently become false — the software was right until the world moved (loc 367). The open questions he opens the book with — correctness under internal failure, graceful degradation, load growth, API shape — are the same questions on-call engineers chase retroactively in RCAs (loc 255).

**Load parameters and the shape of scale.** "Scalability" is not a property a system has (loc 420); it is a function of which load parameter you optimized for (loc 428). Data problems are driven by three pressures — volume, complexity, and rate of change (loc 207) — and the three classical model boundaries (relational / document / graph) are collapsing under those pressures (loc 238). Head-of-line blocking is the default failure mode when a slow request sits in front of fast ones (loc 559).

**Data modeling trade-offs.** The document-vs-relational debate reduces to whether your domain has many-to-many relationships (loc 1169) and whether you want schema-on-read flexibility (loc 1195) or locality for queries (loc 1260). Tree-shaped one-to-many data fits documents cleanly (loc 1028); anything meaningful to humans will change, and duplicated copies become update-anomaly traps (loc 1051) — the motivation for normalization (loc 1053). Without join support in the engine, you end up emulating joins in application code, badly (loc 1068). Impedance mismatch (loc 944) and ORMs (loc 948) remain the connective tissue between object code and tabular storage. Abstractions layer cleanly only when each layer hides a coherent data model from the one above (loc 882).

**Schema evolution is an operational hazard.** Schema-on-write engines vary wildly in how they apply `ALTER TABLE` — MySQL's full-table copy means minutes to hours of downtime on large tables (loc 1244), which is a concrete reason schema-on-read is attractive for heterogeneous object graphs whose structure you do not control (loc 1254).

**Query languages and optimizer leverage.** Declarative SQL wins because it cedes execution choices — index selection, join order, method — to an optimizer (loc 1357); the narrower the language, the more room the engine has to rewrite the plan (loc 1366). MapReduce sits between declarative and imperative: query logic is code snippets invoked by the framework, borrowing map/reduce from functional languages (loc 1478). Graph workloads get their own vocabulary — property graphs for traversal-native queries (loc 1648), and SQL's recursive CTEs for emulating the same walks in relational engines (loc 1790).

**Storage-engine asymmetries.** OLTP and analytics engines diverge sharply, and the split is worth respecting when picking storage (loc 2351). Append-only writes are the cheapest write primitive (loc 2403); every auxiliary structure — including every index — taxes writes to accelerate reads (loc 2404).

## Source

- Kindle highlights: `sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md`
