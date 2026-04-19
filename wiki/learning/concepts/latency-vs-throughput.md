---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md
  - sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md
---

# Latency vs throughput

Parent: [[../index|Learning MOC]] · Sources: [[../books/systems-performance|Gregg]], [[../books/designing-data-intensive-applications|DDIA]]

## The distinction

- **Latency** — time a single operation takes (wait + service).
- **Throughput** — completed operations per unit time.

They're coupled through queueing theory but not interchangeable. Low latency can coexist with low throughput (idle system); high throughput can coexist with bad latency (saturated system with long queues).

## Qualify your latencies

> "Since the single word 'latency' can be ambiguous, it is best to include qualifying terms: request latency, TCP connection latency, etc." — Gregg (loc 1233)

Naming conventions aren't pedantry — they're the only way two engineers in an incident can keep apples and oranges separate.

## Percentiles, not averages

DDIA hammers on this (loc 537, 573): the customers with the slowest 99.9th-percentile requests are often your most valuable customers (they have the most data). Average latency hides them. **Tail latency amplification** compounds this — a service that calls N backends inherits the worst tail of all N.

Gregg's six-inch-stream joke (loc 2455) applies here word-for-word.

## Trade-offs

- CPU ↔ memory: cache results to trade memory for CPU, or compress to trade CPU for memory (Gregg loc 1293).
- Read ↔ write: fan-out-on-write trades publish cost for read latency (DDIA's Twitter example, loc 464).
- Throughput ↔ tail latency: linear scalability of response time sometimes requires returning 503s instead of queueing (Gregg loc 1413).

## Related

- [[use-method|USE method]]
- [[scalability|Scalability]]
- [[golden-signals|Four golden signals]]
