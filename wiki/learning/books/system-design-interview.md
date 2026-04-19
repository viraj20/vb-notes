---
type: source-summary
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Xu-System Design Interview – An insiders guide.md
---

# System Design Interview — An Insider's Guide (Xu)

- Author: Alex Xu
- ASIN: B08B3FWYBX
- Source: Kindle highlights (1 annotation — a compact scaling checklist)

Parent: [[../index|Learning MOC]] · Related: [[designing-data-intensive-applications|DDIA]] · [[site-reliability-engineering|SRE book]]

## The scaling checklist (loc 408)

- Keep the web tier stateless
- Build redundancy at every tier
- Cache data as much as you can
- Support multiple data centers
- Host static assets in CDN
- Scale the data tier by sharding
- Split tiers into individual services
- Monitor your system and use automation tools

## Why it's compact

Only one highlight was captured from this book, but it distills the default playbook most system-design discussions assume. Each bullet maps to a deeper concept:

- Stateless tier → horizontal [[../concepts/scalability|scalability]]
- Redundancy → [[site-reliability-engineering|SRE book]]'s N+1 principle
- Monitoring + automation → [[../concepts/golden-signals|Four golden signals]] and [[../concepts/toil|toil reduction]]
- Sharding → DDIA's [[designing-data-intensive-applications|shared-nothing]] architecture

## Source

- Kindle highlights: `sources/learning/books/Kindle Highlights/Xu-System Design Interview – An insiders guide.md`
