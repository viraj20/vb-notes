---
type: concept
domain: work
status: live
created: 2026-04-20
updated: 2026-04-20
sources:
  - sources/work/projects/on-ground/research/atomx-research.md
---

# Data ontology

Parent: [[index|Shared MOC]] · [[../index|Work MOC]] · Related: [[medallion-data-pipeline|Medallion data pipeline]] · [[canonical-enum-layer|Canonical enum layer]] · [[graph-traversal-hop-depth|Graph traversal & hop depth]] · [[../on-ground/atomx-ontology-design|AtomX ontology design]]

An ontology is a semantic layer sitting on top of cleaned tables. It converts columns into typed objects that applications can query without ever touching the underlying dataset. Palantir Foundry is the reference implementation; the pattern can be built on Databricks, dbt, or plain Postgres.

## The three primitives

**Object type** — a real-world noun backed by a dataset. Examples for AtomX: `Transaction`, `Stall`, `Event`, `Device`, `Customer`, `Item`. Apps never see the dataset, only the object and its typed properties.

**Link type** — a named, directional relationship between two object types. Examples: `Transaction → occurred_at → Stall`, `Transaction → part_of → Event`, `Customer → attended → Event`. All links live in a single central link table.

**Action** — a write-back operation that modifies an object through the ontology, not through a direct DB write. Examples: `mark_as_reversed`, `flag_anomaly`, `trigger_settlement`. Actions are auditable by default — every execution writes to an audit log.

## Why it earns the abstraction

- **Schema insulation** — when a source system renames `AMOUNT` to `TXN_VALUE`, you update the dataset-to-object mapping once. Every downstream dashboard, alert, and app keeps working because they queried `Transaction.amount`, not the raw column.
- **AI-friendliness** — an LLM agent can traverse object relationships to answer natural-language questions without writing raw SQL. Query surface becomes "objects and links" instead of "columns and joins."
- **Cross-source merging** — a single `Event` object can be backed by AtomX transaction data *and* BMS ticketing data simultaneously. The join happens inside the ontology, not in every consumer's query.

## The link table

All relationships collapse into one table:

```sql
CREATE TABLE links (
  from_type  VARCHAR,   -- 'Transaction'
  from_id    VARCHAR,   -- '40291'
  link_type  VARCHAR,   -- 'occurred_at'
  to_type    VARCHAR,   -- 'Stall'
  to_id      VARCHAR    -- 'stall_bira_bar'
);

CREATE INDEX idx_links_traversal
ON links (from_type, link_type, to_id);
```

One row per relationship. A transaction with four outgoing links (stall, event, device, customer) generates four rows.

## Query pattern — anchor, traverse, resolve

Every ontology query has the same three-step shape, regardless of depth:

1. **Anchor** — filter one object type by a property to get a set of IDs.
2. **Traverse** — join the link table on `link_type` to reach a new set of IDs.
3. **Resolve** — join back to an object table to apply property filters and compute aggregates.

Repeat step 2 N times for N hops. See [[graph-traversal-hop-depth|graph traversal & hop depth]] for when relational joins stop being comfortable and a graph DB becomes appropriate.

## When not to adopt

If you have one dataset and one consumer, skip it. The ontology earns its weight when the *number of consumers × rate of schema change* starts creating coordination overhead. Below that threshold, the link table is a second source of truth you have to keep in sync for no payoff.
