---
type: concept
domain: work
status: live
created: 2026-04-20
updated: 2026-04-20
sources:
  - sources/work/projects/on-ground/research/atomx-research.md
---

# Medallion data pipeline

Parent: [[../index|Work MOC]] · Related: [[data-ontology|Data ontology]] · [[canonical-enum-layer|Canonical enum layer]] · [[../../learning/books/designing-data-intensive-applications|DDIA]]

The three-layer pipeline popularised by Databricks and Palantir Foundry: **bronze → silver → gold**. Each layer has a distinct contract and a distinct failure mode.

## The three layers

| Layer | Name | Contract |
|---|---|---|
| Bronze | Raw | Immutable, as-received data. Never modified. Full lineage tracked from source. Stored as Parquet or Delta. |
| Silver | Transform | Pipeline transforms in Python / Spark / SQL. Every output dataset has full lineage back to raw. Incremental builds. |
| Gold | Ontology / objects | Objects backed by datasets. Links define relationships. Typed properties. Actions are write-back operations. |

## The Foundry distinction

Every other data platform stops at the transform layer. Foundry's contribution is the **semantic layer** on top — tabular data becomes typed objects with relationships, and applications never query raw tables. That semantic layer is what [[data-ontology|data ontology]] documents.

## Failure modes by layer

- **Bronze** — silent schema drift. If a vendor renames a column and bronze is not strictly typed, corrupted reads propagate forward. The defence is to keep bronze immutable and validate at the silver boundary.
- **Silver** — dirty-value creep. Cleaning logic lives here and must be idempotent; if cleaning is buried in dashboards instead, every consumer reinvents it. The [[canonical-enum-layer|canonical enum layer]] belongs here.
- **Gold** — stale or ambiguous object definitions. Once applications read from gold, any breaking property change ripples outward. Version object views and deprecate, don't rename.

## Where it lands in BMS

For AtomX, the `atomx-pivot-report` skill already performs validate → clean → build steps as a one-shot batch run. Promoting it to a persistent pipeline gives BMS bronze (S3 / DBFS), silver (Delta Live Tables), and gold (Unity Catalog object views) without introducing a new platform. See [[../projects/atomx-ontology-design|AtomX ontology design]] for the concrete layout.

## When not to adopt

A two-table setup (raw + cleaned) is enough until you have more than one downstream consumer. Don't build gold views for queries that only one dashboard runs.
