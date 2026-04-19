---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md
---

# Fault vs failure

Parent: [[../index|Learning MOC]] · Source: [[../books/designing-data-intensive-applications|DDIA]] (loc 294)

## The distinction

- **Fault** — one component deviates from its spec.
- **Failure** — the system as a whole stops providing its required service.

A disk that returns a read error is a fault. A user who can't check out is a failure. They're not the same event, and confusing them breaks incident response.

## Why it matters

> "It is impossible to reduce the probability of a fault to zero; therefore it is usually best to design fault-tolerance mechanisms that prevent faults from causing failures." — DDIA (loc 294)

The engineering goal is not "no faults" — that's impossible. The goal is the **translation barrier**: keep faults local so they don't cascade into failures.

## Corollaries

- Retries, timeouts, circuit breakers, replication, bulkheads — all translate faults into degraded-but-working states.
- **Accidental complexity** (DDIA loc 685, 696) tends to erode the translation barrier by coupling modules that shouldn't be coupled.
- Software makes environmental assumptions that usually hold, but eventually stop holding (DDIA loc 367) — each broken assumption becomes a new fault class.

## Related

- [[scalability|Scalability]]
- [[../books/designing-data-intensive-applications|DDIA]]
- [[error-budget|Error budget]] — how repeated failures draw down the service's unreliability allowance
