# BSE India — Endpoints & URL Patterns

## Scrip Code Lookup

Given an NSE symbol, find the BSE scrip code:
```
# Search by company name or symbol
https://api.bseindia.com/BseIndiaAPI/api/getScripHeaderData/w?Scrip_cd=<SCRIP_CODE>

# Or use the search API
https://api.bseindia.com/BseIndiaAPI/api/ListofScripData/w?Flag=0&Grp=&Cat=0&scripnm=<SYMBOL>
```

Common scrip codes (examples for testing):
- TCS: 532540
- INFY: 500209
- RELIANCE: 500325
- HDFCBANK: 500180

---

## Corporate Filings — Announcement List

Base URL pattern:
```
https://www.bseindia.com/corporates/ann.html?scrip=<SCRIP_CODE>&Category=<CATEGORY>&subcategory=-1
```

### Category Codes

| What you want | Category value |
|---|---|
| Concall transcripts | `Concall` |
| Analyst/Investor meetings | `Analyst Meet` |
| Financial results (quarterly) | `Result` |
| Annual reports | `Annual%20Report` |
| Board meeting outcomes | `Board Meeting` |
| Shareholding pattern | `Shareholding%20Pattern` |
| All announcements | (omit Category param) |

### Pagination
Add `&page=<N>` to paginate. Default returns ~20 results per page.

### Date filtering
Add `&Fdate=<DD/MM/YYYY>&Tdate=<DD/MM/YYYY>` to filter by date range.

Example — fetch last 2 years of concall transcripts for TCS:
```
https://www.bseindia.com/corporates/ann.html?scrip=532540&Category=Concall&subcategory=-1&Fdate=01/01/2023&Tdate=31/12/2024
```

---

## PDF Download Pattern

All filing attachments follow this URL pattern:
```
https://www.bseindia.com/xml-data/corpfiling/AttachHis/<UUID>.pdf   # historical
https://www.bseindia.com/xml-data/corpfiling/AttachLive/<UUID>.pdf  # recent/live
```

The UUID comes from the announcement list JSON response. These PDFs are publicly
accessible — no auth required.

---

## Direct Company Filing Page

Human-readable page listing all filings for a company:
```
https://www.bseindia.com/corporates/ann.html?scripcd=<SCRIP_CODE>
```

---

## Financial Results API (structured data)

For recent quarterly results in JSON:
```
https://api.bseindia.com/BseIndiaAPI/api/FinancialResults/w?scripcode=<SCRIP_CODE>&period=Quarterly&isconsoliated=on
```

Parameters:
- `period`: `Quarterly` | `Annual`
- `isconsoliated`: `on` | `off` (consolidated vs standalone)

---

## Shareholding Pattern

```
https://api.bseindia.com/BseIndiaAPI/api/ShareHoldingPatterns/w?scripcode=<SCRIP_CODE>&flag=C&fromdate=<YYYY-MM-DD>&todate=<YYYY-MM-DD>
```

Returns promoter %, FII %, DII %, public % by quarter.

---

## Quote (Price Data)

```
https://api.bseindia.com/BseIndiaAPI/api/getScripHeaderData/w?Scrip_cd=<SCRIP_CODE>
```

Returns: CMP, P/E, market cap, 52W high/low, face value, book value.

---

## Required Headers

BSE API calls require these headers to avoid 403/blocking:
```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
Accept: application/json, text/plain, */*
Referer: https://www.bseindia.com/
Origin: https://www.bseindia.com/
```

No cookies required for most read-only endpoints (unlike NSE).

---

## Known Failure Modes

- Large PDFs (annual reports) may timeout — try multiple fetches or fetch page ranges
- Concall category name varies by company — if `Concall` returns empty, try
  `Analyst%20Meet` or fetch all announcements and filter for "transcript" in title
- Some small-cap companies file transcripts under "General" category
- AttachLive vs AttachHis: if a UUID returns 404 on AttachHis, try AttachLive
