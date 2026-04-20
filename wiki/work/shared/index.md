---
type: moc
domain: work
status: live
created: 2026-04-20
updated: 2026-04-20
sources: []
---

# Shared — Work patterns MOC

Cross-project concepts and patterns used by 2+ BMS projects. Sits one level below the work MOC; a level above project folders.

Parent: [[../index|Work MOC]]

## Promotion rule

A page lives here when it applies to more than one project. A page starts in a project folder (`wiki/work/<project>/`) and gets promoted here when a second project links to it. Mirror of the global `wiki/synthesis/` pattern, one scope smaller.

## Data architecture

- [[medallion-data-pipeline|Medallion data pipeline]] — bronze / silver / gold
- [[data-ontology|Data ontology]] — Palantir-style object / link / action model
- [[canonical-enum-layer|Canonical enum layer]] — schema-insulation pattern
- [[graph-traversal-hop-depth|Graph traversal & hop depth]] — SQL link table vs graph DB

_Other sub-areas (SRE practice, reliability patterns, debugging heuristics) will accumulate here as they earn cross-project pull._
