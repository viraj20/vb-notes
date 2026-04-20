---
captured: 2026-04-20
captured_via: ingest-file
original_path: sources/work/projects/on-ground/research/atomx-research.md
wiki_compiled: true
---

# AtomX POS — Data Layer & Ontology Research

> Research compiled from architecture exploration session, April 2026.
> Covers: AtomX system overview, POS technology stack, monitoring approaches, Palantir-style ontology design, technology recommendations, and query patterns.

---

## 1. AtomX System Overview

AtomX is a **closed-loop, stored-value cashless payments platform** built for live events, hospitals, and campuses. It is a BookMyShow portfolio company (strategic investment, 2019).

Key characteristics:

- NFC wristbands, cards, and keychains store digital currency on-chip
- Transaction time under one second
- Works offline — no internet dependency at the point of sale
- Deployed at 180+ events across India and Indonesia
- 4+ lakh unique activations, ₹150+ crore in transactions to date

### Public Documentation Status

AtomX does **not** have publicly available API or developer documentation. No public REST API, no webhook schema, no SDK reference. The primary source of ground truth for BMS is the raw `AtomX-Dataset.xlsx` export and the internal `atomx-pivot-report` skill.

---

## 2. POS Technology Stack

Modern POS systems like AtomX, Pine Labs, and Razorpay PoS share a common layered architecture:

| Layer | Technology |
|---|---|
| Hardware | NFC/EMV chip reader, MSR swipe, barcode scanner, receipt printer, cash drawer |
| Connectivity | Wi-Fi / 4G LTE / Ethernet, Bluetooth LE, USB serial |
| Application | Android (Kotlin/Java) or iOS (Swift), React Native / Flutter, embedded Linux |
| Payment processing | EMV kernel, tokenisation (PCI-DSS), ISO 8583 / REST APIs, acquirer gateway routing |
| Backend / cloud | Node.js / Java / Go microservices, PostgreSQL / Redis, Kafka, AWS / GCP |
| Analytics | Merchant dashboard, webhook events, settlement reconciliation, fraud scoring |

AtomX specifically runs on Android-based terminals with NFC hardware, exposing an SDK that merchant billing apps integrate. Transaction results fire as callbacks in the merchant app.

---

## 3. AtomX Raw Data Schema

The raw `AtomX-Dataset.xlsx` export contains the following columns (exact, case-sensitive):

| Column | Type | Notes |
|---|---|---|
| TXN ID | integer | Unique transaction identifier |
| TYPE | string | sale, topup, reversal_sale, reversal_topup, inventory_deploy |
| STALL NAME | string | Vendor / point of sale name |
| DEVICE | string / integer | POS terminal identifier |
| MODE | string | NFC, CARD, CASH, UPI, INV_BOX |
| MODE INFO | string | Often null |
| RECEIPT | string | Receipt number |
| INVOICE TYPE | string | MENU, CASH, UPI, TAPX, CARD — may have dirty values |
| CARD ID | integer | Customer wristband ID; 0 = anonymous |
| AMOUNT | float | Transaction value in INR |
| LABEL | string | normal or activated |
| STATUS | string | All rows should be `completed` |
| TIMESTAMP | datetime | Transaction datetime |
| ITEMS | string | First item; overflow in Unnamed columns |

### Known Data Quality Issues

- `INVOICE TYPE` may contain Unix timestamps — cleaned to `TIMESTAMP_ERROR`
- Epoch timestamps (`1970-01-01`) appear in inventory rows — dropped at clean step
- `CARD ID = 0` indicates anonymous sales (~24 rows) — flagged, not dropped
- Zero-amount rows (1–5) — flagged, not dropped
- Items overflow into `Unnamed: 15` through `Unnamed: 33` columns — collapsed to `ITEMS_ALL`

---

## 4. The atomx-pivot-report Skill

An internal automation pipeline that processes the raw AtomX export into settlement reports. It runs as a post-event batch process.

### Pipeline Steps

1. **Validate** — confirms required columns, known TYPE values, no duplicate TXN IDs
2. **Clean** — filters inventory rows, fixes dirty values, collapses item columns, adds derived fields (`DATE`, `HOUR`, `STALL_CATEGORY`, `IS_REVERSAL`, `IS_POS_SALE`)
3. **Build report** — produces a two-sheet Excel workbook:
   - **Summary sheet**: Cashless Topups, Cashless Sales, POS Sales, Reversals, Activations, Devices Used
   - **Redemption sheet**: stall-wise breakdown by mode (NFC / CASH / CARD / UPI), plus item-level detail
4. **QA** — verifies report totals tie back to cleaned data
5. **Deliver** — summary of key numbers + links to both output files

### Outputs

- `{EventName}-{YYYYMMDD-HHMM}-Cleaned.csv`
- `{EventName}-{YYYYMMDD-HHMM}-Report.xlsx`

### Limitation

This is a **retrospective, batch tool** — run after an event concludes. It does not provide real-time visibility during an event.

---

## 5. Palantir-Style Data Architecture

### The Medallion Pipeline

Palantir Foundry (and the open-source equivalent) uses a three-layer pipeline:

| Layer | Name | Description |
|---|---|---|
| Bronze | Raw | Immutable, as-received data. Never modified. Full lineage tracked from source. Stored in Parquet / Delta. |
| Silver | Transform | Pipeline transforms in Python / Spark / SQL. Every output dataset has full lineage back to raw. Incremental builds. |
| Gold | Ontology | Objects backed by datasets. Links define relationships. Properties are typed. Actions are write-back operations. |

### What Makes Palantir Different

Every other data platform stops at the transform layer. Palantir adds a **semantic layer** on top that converts tabular data into typed objects with relationships. Applications query objects and links — never raw tables.

---

## 6. The Ontology — Concepts

An ontology has three primitives:

**Object type** — a real-world noun backed by a dataset. Examples: `Transaction`, `Stall`, `Event`, `Device`, `Customer`. Apps never see the dataset, only the object and its properties.

**Link type** — a named, directional relationship between two object types. Examples: `Transaction → occurred_at → Stall`, `Transaction → part_of → Event`. Links are stored in a central link table.

**Action** — a write-back operation that modifies an object through the ontology, not through a direct DB write. Examples: `mark_as_reversed`, `flag_anomaly`, `trigger_settlement`. Actions are auditable by default.

### Why This Matters

- **Schema insulation** — when AtomX changes a column name, you update the dataset-to-object mapping once. Every downstream query, dashboard, and alert keeps working because they queried `Transaction.amount`, not the raw column `AMOUNT`.
- **AI-friendliness** — an AI agent can traverse object relationships to answer natural language questions without writing raw SQL.
- **Cross-source merging** — a single `Event` object can be backed by AtomX transaction data and BMS ticketing data simultaneously.

---

## 7. AtomX Ontology Design

### Object Types

**Transaction** — backed by the cleaned transactions table
Properties: `txn_id`, `amount`, `txn_type` (canonical), `payment_mode` (canonical), `timestamp`, `is_reversal`, `is_pos_sale`, `stall_category`, `receipt`, `items_all`, `label`

**Stall** — derived from distinct STALL NAME values
Properties: `stall_id`, `name`, `category`, `total_sales` (derived), `txn_count` (derived), `top_item` (derived)

**Event** — from BMS event master + AtomX export header
Properties: `event_id`, `name`, `date`, `venue`, `total_activations`, `total_topup_amount`, `total_sales_amount`, `total_reversals`, `unique_customers`, `unique_devices`

**Device** — from distinct DEVICE values
Properties: `device_id`, `txn_count`, `total_processed`, `reversal_count`, `first_seen`, `last_seen`

**Customer** — from distinct CARD ID values (non-zero)
Properties: `card_id`, `total_topup`, `total_spent`, `balance_remaining`, `txn_count`, `first_txn_time`, `label`

**Item** — parsed from ITEMS_ALL
Properties: `item_id`, `name`, `category`, `unit_price`, `total_qty_sold`, `total_revenue`

### Link Types

| From | Link | To | Via |
|---|---|---|---|
| Transaction | occurred_at | Stall | STALL NAME |
| Transaction | part_of | Event | event context |
| Transaction | processed_by | Device | DEVICE |
| Transaction | paid_by | Customer | CARD ID |
| Transaction | contains | Item | ITEMS_ALL parsed |
| Transaction | reversed_by | Transaction | reversal pair self-link |
| Stall | operated_at | Event | — |
| Stall | used | Device | device-stall assignment |
| Device | assigned_to | Stall | — |
| Customer | attended | Event | via activation record |

### Actions

| Object | Actions |
|---|---|
| Transaction | mark_as_reversed, flag_anomaly, add_note, approve_for_settlement |
| Event | close_event, trigger_settlement, export_report |
| Device | mark_offline, reassign_to_stall |
| Customer | issue_refund, flag_suspicious |

---

## 8. The Link Table

All relationships are stored in a single central table:

```sql
CREATE TABLE atomx_ontology.links (
  from_type  VARCHAR,   -- e.g. 'Transaction'
  from_id    VARCHAR,   -- e.g. '40291'
  link_type  VARCHAR,   -- e.g. 'occurred_at'
  to_type    VARCHAR,   -- e.g. 'Stall'
  to_id      VARCHAR    -- e.g. 'stall_bira_bar'
);

-- Index for traversal performance
CREATE INDEX idx_links_traversal
ON atomx_ontology.links (from_type, link_type, to_id);
```

One row per relationship. A transaction with 4 links (stall, event, device, customer) has 4 rows in this table.

### Query Pattern — Anchor → Traverse → Resolve

Every ontology query follows this three-step shape regardless of complexity:

1. **Anchor** — filter one object type by a property to get a set of IDs
2. **Traverse** — join the link table on `link_type` to reach a new set of IDs
3. **Resolve** — join back to an object table to apply property filters and compute aggregates

Repeat the traverse step N times for N hops.

---

## 9. Canonical Enum Layer

Raw AtomX string values are a source of fragility. They must be mapped to a controlled vocabulary at the transform step so all downstream queries use your own enum names — never AtomX's.

### Mapping Tables

**Transaction type**

| AtomX raw value | Canonical value |
|---|---|
| sale | TXN_SALE |
| topup | TXN_TOPUP |
| reversal_sale | TXN_REVERSAL |
| reversal_topup | TXN_REVERSAL |
| inventory_deploy | TXN_INVENTORY |

**Payment mode**

| AtomX raw value | Canonical value |
|---|---|
| NFC | MODE_NFC |
| CARD | MODE_CARD |
| CASH | MODE_CASH |
| UPI | MODE_UPI |
| INV_BOX | MODE_INVENTORY |

### Production Pattern — Config Table

In production, store the mapping as a live Delta table (`atomx_config.enum_mappings`) with `valid_from` / `valid_to` timestamps. The transform reads it at runtime. Adding a new AtomX value requires inserting one row — no code change, no redeployment.

```sql
-- atomx_config.enum_mappings
source_system | field_name | raw_value      | canonical_value | valid_from | valid_to
atomx         | TYPE       | sale           | TXN_SALE        | 2023-01-01 | null
atomx         | TYPE       | purchase       | TXN_SALE        | 2025-06-01 | null  -- new alias
atomx         | MODE       | NFC            | MODE_NFC        | 2023-01-01 | null
```

**Rule**: Raw AtomX strings exist only in the bronze layer and the enum_mappings config table. The silver layer and everything above speaks only the canonical vocabulary.

---

## 10. Graph Traversal — Hop Depth

### Relational vs Graph DB

| Aspect | Relational (SQL link table) | Graph DB (Neo4j, Neptune) |
|---|---|---|
| Relationship storage | Implicit — matching column values | Explicit — pointers on each node |
| Traversal mechanism | JOIN — scans rows, hashes, matches | Pointer follow — O(1) per hop |
| Cost scaling | Grows with table size | Constant regardless of graph size |
| Good at | Aggregations, analytics, large datasets | Deep traversals, shortest paths, variable depth |
| Bad at | 5+ hop traversals, variable-depth paths | Bulk analytics, large aggregations |

### Hop Count Examples

| Question | Hops | SQL comfort |
|---|---|---|
| Stall sales at one event | 2 | Easy |
| Customers at one event by payment mode | 3 | Easy |
| Customers at two events with spend filter | 4 | Manageable |
| Customers at 3+ events with stall overlap | 5–6 | Painful |
| Fraud: customer networks sharing devices | 6+, variable | Very hard |

### The AND Collapse Optimisation

For questions like "customers who spent heavily at both NH7 and Lollapalooza", instead of traversing Event → Transaction → Customer → Transaction → Event (4 hops), anchor on Customer, traverse to all their transactions, filter to both events with `IN (...)`, and use `HAVING COUNT(DISTINCT event_id) = 2` to enforce the intersection.

This collapses 4 hops to 2 hops. The "both events" condition moves from the traversal into the aggregation.

```sql
WITH customer_events AS (
  SELECT
    l_pay.to_id                 AS customer_id,
    l_evt.to_id                 AS event_id,
    SUM(t.amount)               AS spend
  FROM   links        l_pay
  JOIN   links        l_evt
         ON  l_evt.from_id   = l_pay.from_id
         AND l_evt.link_type = 'part_of'
  JOIN   transactions t
         ON  t.txn_id        = l_pay.from_id
  WHERE  l_pay.link_type  = 'paid_by'
    AND  l_evt.to_id      IN ('evt_nh7_2025', 'evt_lolla_2025')
    AND  t.txn_type       = 'TXN_SALE'
  GROUP  BY l_pay.to_id, l_evt.to_id
)
SELECT
  customer_id,
  MAX(CASE WHEN event_id = 'evt_nh7_2025'   THEN spend END) AS nh7_spend,
  MAX(CASE WHEN event_id = 'evt_lolla_2025' THEN spend END) AS lolla_spend
FROM   customer_events
GROUP  BY customer_id
HAVING COUNT(DISTINCT event_id) = 2
   AND MIN(spend) > 5000
ORDER  BY nh7_spend DESC
```

**When the AND collapse works**: fixed set of target values, condition is "did entity appear in all/some of them."

**When it does not work**: two different entities connecting via a shared intermediate (e.g. fraud rings: customer A and B sharing a device across events). That requires genuine multi-hop traversal.

---

## 11. Technology Recommendations

### For BMS — Build on Existing Stack

Do not introduce a new platform. The ontology layer can be built entirely on Databricks, which BMS already operates.

| Layer | Tool | Role |
|---|---|---|
| Ingestion | S3 / DBFS | Raw AtomX exports land as Delta tables (bronze) |
| Transform | Databricks Delta Live Tables | Promotes clean.py logic into a persistent pipeline |
| Ontology | Unity Catalog + dbt models | Object type definitions, lineage, governance |
| Links | Delta table (`atomx_ontology.links`) | Central relationship store |
| Enum mapping | Delta table (`atomx_config.enum_mappings`) | Canonical vocabulary config |
| Monitoring | Grafana / Metabase | Queries run against object views, not raw tables |
| AI layer | Claude API | Natural language → SQL against ontology views |
| Actions | FastAPI service | Write-back with audit log to `atomx_actions` table |

### Technology Options Evaluated

**Palantir Foundry** — the reference implementation. Purpose-built for this workflow but expensive (seven-figure contracts) and closed-source. Not recommended for BMS scale.

**Apache Atlas + Databricks Unity Catalog** — open-source metadata/lineage on top of existing Databricks. Lowest-friction path. Recommended.

**dbt + Neo4j** — dbt models as object definitions, Neo4j for graph traversal. Engineer-friendly if team knows SQL/dbt. Useful if deep traversal queries emerge.

**Microsoft Fabric** — OneLake + semantic layer. Reasonable alternative if org is Azure-aligned.

**Atlan / DataHub** — metadata catalog tools. Good for discovery and governance, not for building apps on top of the ontology.

### When to Add a Graph DB

Introduce Neo4j or Apache Neptune when questions require:
- 5+ hop traversals
- Variable-depth path queries
- Shortest path calculations
- Influence network analysis (fraud rings, cross-customer device sharing)

For AtomX today, the Delta link table handles all known use cases. Graph DB is a future upgrade path, not an immediate requirement.

---

## 12. Recommended Next Steps

1. **Promote clean.py to a Delta Live Tables pipeline** — replace the manual post-event run with a scheduled or triggered Databricks pipeline that populates `atomx_silver.*` tables persistently.

2. **Create the link table** — build `atomx_ontology.links` populated by a transform that joins the silver tables and emits one row per relationship.

3. **Build the enum mapping config table** — migrate the TYPE_MAP and MODE_MAP dicts from clean.py into `atomx_config.enum_mappings` with versioning support.

4. **Define object views** — create SQL views on top of the silver tables that expose canonical property names (`txn_type`, `payment_mode` etc.) to downstream consumers.

5. **Wire a live monitoring dashboard** — Grafana or Metabase querying the object views. Key metrics: transaction success rate by device, NFC vs cash split by stall, reversal rate per event, stall-wise revenue in real time.

6. **Evaluate graph DB trigger** — if cross-event loyalty analysis or fraud network detection becomes a requirement, evaluate Apache AGE (graph extension for Postgres) or Neo4j alongside the existing Databricks stack.

---

*Document generated from architecture research session. All schema details derived from the internal atomx-pivot-report skill and AtomX-Dataset.xlsx column definitions.*
