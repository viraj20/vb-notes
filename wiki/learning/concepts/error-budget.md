---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md
---

# Error budget

Parent: [[../index|Learning MOC]] · Source: [[../books/site-reliability-engineering|SRE book]]

## Definition

The allowable unreliability of a service over a period, set by its SLO. If the SLO is 99.9% availability, the error budget is 0.1% — that's the unreliability the business has authorized.

## Why it matters

The error budget reframes SRE's mission. The goal is **not zero outages** — zero outages means either the SLO is too lax or feature velocity is being over-sacrificed. Instead:

> "SRE's goal is no longer 'zero outages'; rather, SREs and product developers aim to spend the error budget getting maximum feature velocity." — SRE book (loc 439)

## Mechanics

- **Spent** by any unavailability, planned or unplanned (launches, experiments, bugs, outages).
- **Budget-aware release policy** — when burn is within budget, ship fast; when exceeded, freeze risky releases until reliability is recovered.
- **Shared incentive** — dev and SRE teams agree on the SLO and share the budget, resolving the classic dev-vs-ops friction (loc 316).

## Related

- [[toil|Toil]] — the work that erodes the budget
- [[golden-signals|Four golden signals]] — how burn is measured
- [[../books/site-reliability-engineering|SRE book]] — full treatment
- [[../../synthesis/sre-practice-for-bms|SRE practice for BMS]] — application context
