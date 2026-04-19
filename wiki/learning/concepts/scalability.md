---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Kleppmann-Designing Data-Intensive Applications.md
  - sources/learning/books/Kindle Highlights/Xu-System Design Interview – An insiders guide.md
---

# Scalability

Parent: [[../index|Learning MOC]] · Sources: [[../books/designing-data-intensive-applications|DDIA]], [[../books/system-design-interview|Xu]]

## Definition

> "Scalability is the term we use to describe a system's ability to cope with increased load." — DDIA (loc 420)

Scalability isn't a property; it's a question about a *specific load parameter* growing in a *specific way*. The right parameters depend on the system: RPS, read/write ratio, concurrent users, cache hit rate, data volume per account.

## Load-parameter-shaped architecture

> "An architecture that scales well for a particular application is built around assumptions of which operations will be common and which will be rare — the load parameters." — DDIA (loc 626)

Twitter's fan-out-on-write (DDIA loc 464) is a classic example: publish rate is two orders of magnitude below timeline-read rate, so it's cheaper to do work at write time.

## Scale-up vs scale-out

> "Common wisdom until recently was to keep your database on a single node (scale up) until scaling cost or high-availability requirements forced you to make it distributed." — DDIA (loc 615)

**Shared-nothing** (DDIA loc 605) is the default horizontal pattern — each node has its own CPU, memory, and disk.

## Xu's scaling checklist

Alex Xu's one-highlight compression (loc 408) of the default playbook:

- Stateless web tier · redundancy everywhere · aggressive caching · multi-DC · CDN for static · shard the data tier · split into services · monitor & automate

## Related

- [[latency-vs-throughput|Latency vs throughput]]
- [[fault-vs-failure|Fault vs failure]]
- [[use-method|USE method]]
- [[../books/designing-data-intensive-applications|DDIA]]
- [[../books/system-design-interview|System Design Interview]]
