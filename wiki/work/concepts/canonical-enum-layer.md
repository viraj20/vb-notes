---
type: concept
domain: work
status: live
created: 2026-04-20
updated: 2026-04-20
sources:
  - sources/work/projects/on-ground/research/atomx-research.md
---

# Canonical enum layer

Parent: [[../index|Work MOC]] · Related: [[data-ontology|Data ontology]] · [[medallion-data-pipeline|Medallion data pipeline]] · [[../tools/atomx|AtomX]]

A schema-insulation pattern: raw string values from a source system are mapped to a controlled vocabulary at the transform step, so everything downstream speaks your own enum names — never the vendor's.

## The problem

External systems emit free-form strings. AtomX emits `sale`, `topup`, `reversal_sale`, `reversal_topup`, `inventory_deploy`. The second AtomX renames one of these — or the second a new alias appears (`purchase` instead of `sale`) — every downstream query that filtered on the raw string silently breaks or, worse, silently excludes the new rows.

## The pattern

Map raw values to canonical values at the silver transform. Downstream reads speak canonical-only.

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

## Config-as-data, not code

In production, store the mapping as a live Delta table with validity windows, not a Python dict:

```sql
-- atomx_config.enum_mappings
source_system | field_name | raw_value | canonical_value | valid_from | valid_to
atomx         | TYPE       | sale      | TXN_SALE        | 2023-01-01 | null
atomx         | TYPE       | purchase  | TXN_SALE        | 2025-06-01 | null  -- new alias
atomx         | MODE       | NFC       | MODE_NFC        | 2023-01-01 | null
```

Adding a new raw value becomes one row insert — no code change, no redeployment, no Spark job rebuild.

## The rule

Raw vendor strings exist in **only two places**: the bronze layer and the `enum_mappings` config table. The silver layer and everything above speaks canonical vocabulary only. Violations of this rule are what cause "we thought we had it, then a rename broke three dashboards at once."

## Testing discipline

The mapping table is itself a contract. Add a test that asserts every distinct raw value seen in bronze has a row in `enum_mappings` — anything unmapped should fail CI and block the silver build, not get silently converted to NULL.
