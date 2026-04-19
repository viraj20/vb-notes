---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md
---

# Four golden signals

Parent: [[../index|Learning MOC]] · Source: [[../books/site-reliability-engineering|SRE book]] (loc 1379)

## The four

1. **Latency** — time to serve a request (split success vs error paths; slow errors are still expensive).
2. **Traffic** — demand on the system in its natural unit (RPS, transactions/sec, concurrent sessions).
3. **Errors** — rate of failed requests; distinguish explicit, implicit (wrong-content 200s), and policy (SLA breaches).
4. **Saturation** — how "full" the service is; the constrained resource that determines when latency/error growth will kick in.

## Monitoring taxonomy

SRE book (loc 450) distinguishes three valid outputs from a monitoring system:

- **Alerts** — a human must act *immediately*.
- **Tickets** — a human must act *soon* (days).
- **Logs** — no one reads them unless something else prompts them.

And the prime directive:

> "Monitoring should never require a human to interpret any part of the alerting domain. Instead, software should do the interpreting, and humans should be notified only when they need to take action." (loc 447)

## Relationship to USE

The [[use-method|USE method]] (Utilization, Saturation, Errors) is the resource-level analogue. Golden signals observe service behavior; USE observes the resources underneath.

## Related

- [[use-method|USE method]]
- [[error-budget|Error budget]]
- [[../books/site-reliability-engineering|SRE book]]
- [[../books/systems-performance|Systems Performance]]
