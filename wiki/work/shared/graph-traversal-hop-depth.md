---
type: concept
domain: work
status: live
created: 2026-04-20
updated: 2026-04-20
sources:
  - sources/work/projects/on-ground/research/atomx-research.md
---

# Graph traversal & hop depth

Parent: [[index|Shared MOC]] · [[../index|Work MOC]] · Related: [[data-ontology|Data ontology]] · [[../../learning/books/designing-data-intensive-applications|DDIA]]

When does a relational link table stop being the right substrate, and when does a graph DB (Neo4j, Neptune, Apache AGE) start earning its complexity? The heuristic is **hop depth**.

## Relational vs graph — the storage difference

| Aspect | SQL link table | Graph DB |
|---|---|---|
| Relationship storage | Implicit — matching column values | Explicit — pointers on each node |
| Traversal mechanism | JOIN — scans rows, hashes, matches | Pointer follow — O(1) per hop |
| Cost scaling | Grows with table size | Constant regardless of graph size |
| Good at | Aggregations, analytics, large datasets | Deep traversals, shortest paths, variable depth |
| Bad at | 5+ hop traversals, variable-depth paths | Bulk analytics, large aggregations |

## Hop count as decision rule

| Question | Hops | SQL comfort |
|---|---|---|
| Stall sales at one event | 2 | Easy |
| Customers at one event by payment mode | 3 | Easy |
| Customers at two events with a spend filter | 4 | Manageable |
| Customers at 3+ events with stall overlap | 5–6 | Painful |
| Fraud: customer networks sharing devices | 6+, variable | Very hard |

## The AND collapse optimisation

For a class of multi-hop questions — "customers who spent at *both* NH7 and Lollapalooza" — the naïve traversal is Event → Transaction → Customer → Transaction → Event, four hops. The trick: anchor on Customer, pull every transaction, filter events with `IN (...)`, then use `HAVING COUNT(DISTINCT event_id) = 2` to enforce the intersection. Four hops collapse to two. The "both events" constraint moves from the traversal into the aggregation.

```sql
WITH customer_events AS (
  SELECT l_pay.to_id AS customer_id,
         l_evt.to_id AS event_id,
         SUM(t.amount) AS spend
  FROM   links l_pay
  JOIN   links l_evt ON l_evt.from_id = l_pay.from_id
                    AND l_evt.link_type = 'part_of'
  JOIN   transactions t ON t.txn_id = l_pay.from_id
  WHERE  l_pay.link_type = 'paid_by'
    AND  l_evt.to_id IN ('evt_nh7_2025','evt_lolla_2025')
    AND  t.txn_type = 'TXN_SALE'
  GROUP  BY l_pay.to_id, l_evt.to_id
)
SELECT customer_id,
       MAX(CASE WHEN event_id='evt_nh7_2025'   THEN spend END) AS nh7_spend,
       MAX(CASE WHEN event_id='evt_lolla_2025' THEN spend END) AS lolla_spend
FROM   customer_events
GROUP  BY customer_id
HAVING COUNT(DISTINCT event_id) = 2
   AND MIN(spend) > 5000
```

### When AND collapse works

Fixed set of target values. Condition is "did the entity appear in all / some of them."

### When it does not work

Two different entities connecting via a shared intermediate — e.g. fraud rings where customer A and customer B share a device across events. That requires genuine multi-hop traversal; the AND collapse cannot express it. This is the practical boundary at which introducing a graph DB starts paying for itself.

## Default recommendation

Start with a SQL link table. Evaluate graph DB only when you hit 5+ hop variable-depth questions or shortest-path / influence-network use cases. For AtomX today, the Delta link table covers every known query; graph DB is a future upgrade path, not an immediate requirement.
