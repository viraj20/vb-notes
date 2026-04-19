---
type: synthesis
domain: synthesis
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md
  - sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md
  - sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md
  - sources/learning/books/Kindle Highlights/Xu-System Design Interview – An insiders guide.md
---

# SRE practice for BMS

Parent: [[index|Synthesis MOC]] · Bridges: [[../learning/index|Learning]] ↔ [[../work/index|Work]]

## Purpose

Cross-domain page: how the canonical SRE texts ([[../learning/books/site-reliability-engineering|Murphy et al.]], [[../learning/books/designing-data-intensive-applications|Kleppmann]], [[../learning/books/systems-performance|Gregg]], [[../learning/books/system-design-interview|Xu]]) map onto BookMyShow's context — high-traffic ticketing, bursty event-driven load (Coldplay-style drops), India-scale infrastructure.

As BMS-specific pages accumulate in [[../work/index|work/]], this page should become the junction that links them back to the underlying principle.

## Concept → application grid

| Concept (learning) | BMS application (work — to be populated) |
|---|---|
| [[../learning/concepts/error-budget|Error budget]] | Per-service SLOs (booking, checkout, show-listing). Coldplay-scale drops as budget-aware release gates. |
| [[../learning/concepts/toil|Toil]] | On-call load during ticket drops; automation of common runbook steps. |
| [[../learning/concepts/golden-signals|Golden signals]] | Checkout latency, booking-success rate, queue depth, traffic from app vs web. |
| [[../learning/concepts/use-method|USE method]] | Applied to RDS, Redis, payment-gateway connections during peak. |
| [[../learning/concepts/scalability|Scalability]] | Fan-out-on-write vs on-read decisions in show-availability caches. |
| [[../learning/concepts/fault-vs-failure|Fault vs failure]] | Payment-provider faults contained so booking doesn't fail. |
| [[../learning/concepts/latency-vs-throughput|Latency vs throughput]] | Tail latency on checkout under queue pressure. |

## Open questions for the wiki to answer over time

- What are BMS's current SLOs and how were they chosen?
- Which outages in the last year consumed the most error budget, and why?
- Which services have the worst toil-per-engineer ratio?
- Where does tail-latency amplification bite — which downstream calls are the worst offenders?

These are synthesis prompts: each becomes a page (in `work/`) as the wiki grows, linking back to the underlying concept page here.

## Related

- [[../work/index|Work MOC]]
- [[../learning/index|Learning MOC]]
- [[index|Synthesis MOC]]
