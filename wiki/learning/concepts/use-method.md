---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md
---

# USE method

Parent: [[../index|Learning MOC]] · Source: [[../books/systems-performance|Systems Performance]] (Gregg)

## The method

For every resource, check three metrics:

- **Utilization** — proportion of capacity in use (busy time ÷ total time).
- **Saturation** — degree to which work is waiting (queue length, queued time).
- **Errors** — error count (disk I/O errors, packet drops, exceptions).

Appendix A of *Systems Performance* gives the full Linux checklist.

## Why saturation matters

> "Any degree of saturation is a performance issue, as time is spent waiting (latency)." — Gregg (loc 1473)

Utilization below 100% doesn't mean "healthy"; it just means the daily average hid the burst that queued requests. Averaging hides:

- **60% threshold** — above this, short 100% bursts often lurk undetected (loc 1894).
- **Toll plaza metaphor** (loc 1815) — 40% daily utilization says nothing about rush hour.
- **Stream of six inches** (loc 2455) — averages kill.

## Suggested methodology order

> "Performance monitoring, the USE method, profiling, micro-benchmarking, and static performance tuning." (loc 6492)

Start with what's running; only escalate to profiling and micro-benchmarks once USE has isolated a suspect resource.

## Related

- [[golden-signals|Four golden signals]] — service-level analogue
- [[latency-vs-throughput|Latency vs throughput]]
- [[../books/systems-performance|Systems Performance]]
