---
type: entity
domain: work
status: live
created: 2026-04-20
updated: 2026-04-20
sources:
  - sources/work/projects/on-ground/research/atomx-research.md
---

# AtomX

Parent: [[index|On-ground MOC]] · [[../index|Work MOC]] · Related: [[../shared/data-ontology|Data ontology]] · [[atomx-ontology-design|AtomX ontology design]]

AtomX is a closed-loop, stored-value cashless payments platform built for live events, hospitals, and campuses. BookMyShow strategic investment, 2019.

## What it is

- NFC wristbands, cards, keychains store digital currency on-chip
- Transaction time under one second
- Works offline — no internet dependency at point of sale
- 180+ events across India and Indonesia, 4+ lakh unique activations, ₹150+ crore cumulative value

## Stack

Android-based terminals with NFC hardware. Merchant billing apps integrate the AtomX SDK; transaction results fire as callbacks. Typical POS layering (hardware → connectivity → app → payment processing → backend → analytics) applies.

## Documentation reality

AtomX does **not** publish API or developer documentation. No public REST API, no webhook schema, no SDK reference. Ground truth at BMS is the raw `AtomX-Dataset.xlsx` export plus the internal `atomx-pivot-report` skill — a retrospective, batch pipeline that validates, cleans, builds a settlement report, QAs, and delivers.

## Raw data — columns to know

`TXN ID`, `TYPE` (sale / topup / reversal_sale / reversal_topup / inventory_deploy), `STALL NAME`, `DEVICE`, `MODE` (NFC / CARD / CASH / UPI / INV_BOX), `RECEIPT`, `INVOICE TYPE`, `CARD ID` (0 = anonymous), `AMOUNT`, `LABEL` (normal / activated), `STATUS`, `TIMESTAMP`, `ITEMS`.

Known dirty patterns: Unix timestamps appearing in `INVOICE TYPE` (cleaned to `TIMESTAMP_ERROR`); epoch `1970-01-01` rows in inventory (dropped); item overflow into `Unnamed: 15–33` columns (collapsed to `ITEMS_ALL`). Zero-amount and `CARD ID = 0` rows are flagged, not dropped.

## Why it matters for BMS

Event-scale cashless data has a tight dependency on schema stability — AtomX column names and string enums are the failure surface. See [[../shared/canonical-enum-layer|Canonical enum layer]] for the schema insulation pattern and [[atomx-ontology-design|AtomX ontology design]] for the proposed object model.
