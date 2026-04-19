---
type: moc
domain: synthesis
status: live
created: 2026-04-18
updated: 2026-04-18
sources: []
---

# Home

Daily landing page. The wiki lives at [[wiki/index|Wiki Index]].

## Today

- Today's journal → open the Daily Journal plugin (or `journal/daily/YYYY-MM-DD.md`)
- Inbox depth: `dv = inbox count` (see Dataview block below)

## Wiki domains

- [[wiki/work/index|Work]]
- [[wiki/finances/index|Finances]]
- [[wiki/learning/index|Learning]]
- [[wiki/entertainment/index|Entertainment]]
- [[wiki/ideas/index|Ideas]]
- [[wiki/synthesis/index|Synthesis (cross-domain)]]

## Inbox waiting for classification

```dataview
LIST
FROM "inbox"
WHERE file.name != "urls" AND file.name != "README"
SORT file.mtime DESC
LIMIT 20
```

## Recent wiki activity

```dataview
TABLE file.mtime AS "Updated", domain, status
FROM "wiki"
WHERE type != "moc"
SORT file.mtime DESC
LIMIT 10
```

## Tracker blocks (post-migration paths)

These blocks will populate once `/audit-vault --execute` has moved journals to `journal/daily/`.

```tracker
searchType: frontmatter
searchTarget: exercise
folder: "/journal/daily/"
datasetName: Exercise
month:
```

```tracker
searchType: frontmatter
searchTarget: reading
folder: "/journal/daily/"
datasetName: Reading
month:
```

```tracker
searchType: frontmatter
searchTarget: Expense
datasetName: Money
folder: "/journal/daily/"
line:
    title: Expense
    yAxisLabel: Rs
    yAxisUnit: Rupees
    lineColor: blue
```

## Tasks

```tasks
due this week
```

```tasks
no due date
not done
heading does not include Daily Tasks
```

## Operation log

See [[wiki/log|wiki/log.md]] for the full chronological record.
