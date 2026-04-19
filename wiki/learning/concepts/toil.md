---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md
---

# Toil

Parent: [[../index|Learning MOC]] · Source: [[../books/site-reliability-engineering|SRE book]]

## Definition

Manual, repetitive, automatable, tactical, devoid-of-enduring-value work that scales linearly with service growth. Toil is what fills a team's hours when engineering investment is deferred.

## The scaling problem

> "Running a service with a team that relies on manual intervention … becomes expensive as the service grows, because the size of the team necessarily scales with the load." — SRE book (loc 314)
>
> "Without constant engineering, operations load increases and teams will need more people just to keep pace with the workload." (loc 358)

Toil doesn't just cost salaries — it crowds out the project work that would have eliminated it.

## Budget signal

> "SREs should receive a maximum of two events per 8–12-hour on-call shift." (loc 409)

More than two events is the symptom; the cause is un-paid-down automation debt.

## Antidotes

- Automate change management: progressive rollouts, fast detection, safe rollback (loc 472 — 70% of outages come from changes).
- Playbooks for residual human response (loc 463: ~3× MTTR improvement).
- Cap toil as a fraction of SRE time (the book's 50% target is the classic guideline).

## Related

- [[error-budget|Error budget]] — toil burns the reliability dividend
- [[golden-signals|Four golden signals]] — what on-call should actually be paged for
- [[../books/site-reliability-engineering|SRE book]]
