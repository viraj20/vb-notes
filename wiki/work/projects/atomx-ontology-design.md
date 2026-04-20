---
type: concept
domain: work
status: draft
created: 2026-04-20
updated: 2026-04-20
sources:
  - sources/work/projects/on-ground/research/atomx-research.md
---

# AtomX ontology design

Parent: [[../index|Work MOC]] · Related: [[../tools/atomx|AtomX]] · [[../concepts/data-ontology|Data ontology]] · [[../concepts/medallion-data-pipeline|Medallion data pipeline]] · [[../concepts/canonical-enum-layer|Canonical enum layer]] · [[../concepts/graph-traversal-hop-depth|Graph traversal & hop depth]]

A proposal for promoting the batch `atomx-pivot-report` pipeline into a persistent medallion + ontology layer on BMS's existing Databricks stack. Draft — not yet approved.

## Object types

**Transaction** — backed by cleaned transactions table. Properties: `txn_id`, `amount`, `txn_type` (canonical), `payment_mode` (canonical), `timestamp`, `is_reversal`, `is_pos_sale`, `stall_category`, `receipt`, `items_all`, `label`.

**Stall** — distinct `STALL NAME` values. Properties: `stall_id`, `name`, `category`, plus derived `total_sales`, `txn_count`, `top_item`.

**Event** — BMS event master joined with AtomX export header. Properties: `event_id`, `name`, `date`, `venue`, `total_activations`, `total_topup_amount`, `total_sales_amount`, `total_reversals`, `unique_customers`, `unique_devices`.

**Device** — distinct `DEVICE` values. Properties: `device_id`, `txn_count`, `total_processed`, `reversal_count`, `first_seen`, `last_seen`.

**Customer** — distinct non-zero `CARD ID` values. Properties: `card_id`, `total_topup`, `total_spent`, `balance_remaining`, `txn_count`, `first_txn_time`, `label`.

**Item** — parsed from `ITEMS_ALL`. Properties: `item_id`, `name`, `category`, `unit_price`, `total_qty_sold`, `total_revenue`.

## Link types

| From | Link | To |
|---|---|---|
| Transaction | occurred_at | Stall |
| Transaction | part_of | Event |
| Transaction | processed_by | Device |
| Transaction | paid_by | Customer |
| Transaction | contains | Item |
| Transaction | reversed_by | Transaction (self-link) |
| Stall | operated_at | Event |
| Stall | used | Device |
| Device | assigned_to | Stall |
| Customer | attended | Event |

## Actions

| Object | Actions |
|---|---|
| Transaction | mark_as_reversed, flag_anomaly, add_note, approve_for_settlement |
| Event | close_event, trigger_settlement, export_report |
| Device | mark_offline, reassign_to_stall |
| Customer | issue_refund, flag_suspicious |

Every action writes an audit row to `atomx_actions` — who, when, which object, before/after state.

## Stack mapping

| Layer | Tool | Role |
|---|---|---|
| Ingestion | S3 / DBFS | Raw AtomX exports land as Delta tables (bronze) |
| Transform | Databricks Delta Live Tables | Promotes `clean.py` into a persistent pipeline |
| Ontology | Unity Catalog + dbt models | Object type definitions, lineage, governance |
| Links | Delta table (`atomx_ontology.links`) | Central relationship store |
| Enum mapping | Delta table (`atomx_config.enum_mappings`) | Canonical vocabulary config |
| Monitoring | Grafana / Metabase | Dashboards query object views, not raw tables |
| AI layer | Claude API | Natural language → SQL against ontology views |
| Actions | FastAPI service | Write-back with audit log to `atomx_actions` |

No new platform. Everything BMS already runs.

## Platform options evaluated

- **Palantir Foundry** — reference implementation. Purpose-built but seven-figure contracts and closed-source. Not recommended at BMS scale.
- **Apache Atlas + Databricks Unity Catalog** — open-source metadata/lineage on existing Databricks. Lowest-friction path. **Recommended.**
- **dbt + Neo4j** — dbt models as object definitions, Neo4j for graph traversal. Useful *if* deep-traversal questions emerge; see [[../concepts/graph-traversal-hop-depth|hop depth]].
- **Microsoft Fabric** — OneLake + semantic layer. Reasonable alternative only if the org becomes Azure-aligned.
- **Atlan / DataHub** — metadata catalogs. Good for discovery and governance, not for building apps on top.

## Sequenced next steps

1. Promote `clean.py` to a Delta Live Tables pipeline. Replace the manual post-event run with a scheduled / triggered pipeline writing to `atomx_silver.*`.
2. Create `atomx_ontology.links` populated by a transform that joins silver tables and emits one row per relationship.
3. Migrate `TYPE_MAP` and `MODE_MAP` from `clean.py` into `atomx_config.enum_mappings` with validity windows. See [[../concepts/canonical-enum-layer|canonical enum layer]].
4. Define object views over silver exposing canonical property names (`txn_type`, `payment_mode`).
5. Wire a live monitoring dashboard in Grafana / Metabase against the object views. Key metrics: transaction success rate by device, NFC vs cash split by stall, reversal rate per event, stall-wise revenue.
6. Re-evaluate graph DB trigger when cross-event loyalty or fraud-network detection becomes a concrete requirement.

## Known limitation today

The existing `atomx-pivot-report` skill is a retrospective batch tool — it runs after an event concludes. No real-time visibility during an event. The persistent pipeline in step 1 is what closes that gap.
