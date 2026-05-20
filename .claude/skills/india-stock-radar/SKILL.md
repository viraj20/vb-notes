---
name: india-stock-radar
description: >
  Deep fundamental research skill for NSE/BSE listed Indian stocks. Use this skill
  whenever the user asks to analyse, research, evaluate, or investigate any Indian
  stock or company listed on NSE or BSE — even if they just mention a ticker symbol,
  company name, or ask "is X a good company?". Invoke as /stock-radar <NSE_SYMBOL>.
  Produces a structured, fully-cited .md research file grounded entirely in official
  BSE filings, NSE data, annual reports, and concall transcripts. Never hallucinate
  metrics — every number must carry a [Source | Date] tag or be marked as unavailable.
argument-hint: <NSE_SYMBOL>
compatibility:
  tools: [web_fetch, web_search, bash]
---

# India Stock Radar

A fundamental research skill for Indian equities. Grounds every claim in official
BSE/NSE filings. No buy/sell/hold verdicts. No target prices. No hallucinated numbers.

**Output:** A single timestamped `.md` file saved to the working directory.
**Invoke:** `/stock-radar <NSE_SYMBOL>` e.g. `/stock-radar SHAKTIPUMP`

---

## Hard Rules (Never Break These)

1. **No recommendations.** Banned words: buy, sell, hold, multibagger, undervalued,
   overvalued, target price, strong buy. Violations make the output useless.
2. **Every metric needs a source tag.** Format: `[Source | DD-Mon-YYYY]`
   e.g. `Revenue ₹1,240 Cr [BSE Filing Q3FY25 | 15-Jan-2025]`
3. **Failed fetches = explicit gap, never a guess.** Write
   `[Data unavailable — verify manually]` rather than filling in from memory.
4. **Consolidated financials by default.** Note explicitly if only standalone is
   available.
5. **Red flags and positives must be called out prominently** — not buried in prose.
   Use 🚩 and ✅ markers throughout.
6. **Primary sources rank above everything.** BSE filings > NSE data > Annual Report
   PDFs > news articles > web summaries. Never use a secondary source when the
   primary is fetchable.

---

## Phase 0 — Entity Resolution

Before fetching any data, resolve the exact entity. This prevents name-match errors
(e.g. "Indiabulls" matching 4 different companies).

Fetch and confirm:
- Full legal company name
- NSE symbol (canonical)
- BSE scrip code (6-digit) — needed for filing URLs
- ISIN
- Sector and industry classification
- F&O listed: Yes / No
- Reporting basis available: Consolidated / Standalone-only (flag if latter)

**How to get BSE scrip code from NSE symbol:**
```
https://www.bseindia.com/stock-share-price/<company-slug>/<nse-symbol>/
```
Or search: `https://api.bseindia.com/BseIndiaAPI/api/ComHeader/w?quotetype=EQ&scripcode=<code>`

Once scrip code is confirmed, proceed to Phase 1.

---

## Phase 1 — Parallel Data Fetch (Run All 5 Simultaneously)

### Agent A — Price & Market Data (NSE)

Fetch from NSE official endpoints. Use correct session headers (NSE requires a
prior hit on the homepage to set cookies before API calls work).

Key endpoints:
```
# Homepage first (sets cookies)
GET https://www.nseindia.com/

# Quote data
GET https://www.nseindia.com/api/quote-equity?symbol=<SYMBOL>

# Shareholding pattern
GET https://www.nseindia.com/api/corporate-shareholding-pattern?symbol=<SYMBOL>&series=EQ&from=<DD-MM-YYYY>&to=<DD-MM-YYYY>
```

Extract: CMP, 52W high/low, market cap, P/E (TTM), P/B, dividend yield,
delivery %, face value, listed date.

If NSE fetch fails, fallback: `web_fetch https://www.moneycontrol.com/india/stockpricequote/<sector>/<company>/<symbol>`

---

### Agent B — 10-Year Financials

**Primary: BSE Financial Results filings**

BSE filings list for a scrip (filter by category "Financial Results"):
```
GET https://www.bseindia.com/corporates/ann.html?scrip=<SCRIP_CODE>&Category=Result&subcategory=-1
```

Each quarterly result is a PDF. Fetch the last 8–12 quarters of result PDFs to
extract reported numbers. Parse for: Revenue, EBITDA, PAT, EPS.

**Fallback for 10-year trend: Screener.in HTML**
```
web_fetch https://www.screener.in/company/<NSE_SYMBOL>/consolidated/
```
Extract the 10-year table from the page. Tag all Screener data as:
`[Screener.in — verify against BSE filings | <fetch date>]`

**Mark data confidence:**
- `[Confidence: HIGH]` — sourced from BSE result PDFs
- `[Confidence: MEDIUM]` — sourced from Screener.in HTML
- `[Confidence: LOW]` — sourced from any other aggregator

**Metrics to extract (10-year where available):**

| Metric | What to flag |
|---|---|
| Revenue (₹ Cr) | CAGR 3Y / 5Y / 10Y |
| EBITDA & margin % | Margin compression/expansion trend |
| PAT (₹ Cr) | CAGR 3Y / 5Y / 10Y |
| EPS (₹) | Dilution check — shares outstanding trend |
| ROE % | Sustained above 15% = positive |
| ROCE % | Vs cost of capital (proxy: 10-12%) |
| Debt-to-Equity | Trend direction matters as much as level |
| Interest Coverage | Below 2x = 🚩 |
| Free Cash Flow | FCF = Operating CF − Capex |
| OCF vs PAT | Large sustained divergence = 🚩 |
| Working Capital Days | Increasing = possible stress |

**Automatic flags:**
- D/E > 1.5x and rising → 🚩 High and growing debt
- Interest coverage < 2x → 🚩 Debt servicing risk
- PAT growing but OCF flat/negative for 2+ years → 🚩 Earnings quality concern
- Revenue CAGR > PAT CAGR over 5Y → note margin pressure
- ROE > 20% sustained without high leverage → ✅ Capital efficient

---

### Agent C — Concall Intelligence (Adaptive Depth)

**Source: BSE filings — category "Analyst Meet/Con. Call"**

Step 1: Fetch the announcement list filtered by concall category:
```
web_fetch https://www.bseindia.com/corporates/ann.html?scrip=<SCRIP_CODE>&Category=Concall&subcategory=-1
```
Also try category label variations: "Analyst Meet", "Con. Call Transcript", "Investor Presentation".

Step 2: Identify PDF links. Pattern:
```
https://www.bseindia.com/xml-data/corpfiling/AttachHis/<uuid>.pdf
```

Step 3: **Start with last 4 quarters.** Read each transcript PDF fully.

Step 4: **Adaptive depth trigger** — If after reading 4 quarters the fundamentals
from Agent B show ANY of the following, automatically fetch up to 8 quarters:
- Revenue CAGR 3Y > 15%
- ROE > 18% sustained
- Debt declining while growth is strong
- Major capex or capacity expansion in progress
- Significant business model change in last 2 years

If depth is extended, note: `[Extended to <N> quarters — fundamentals warranted deeper review]`

**Per concall, extract:**

| Section | What to capture |
|---|---|
| Management guidance | Exact revenue/margin/growth targets stated |
| Guidance vs actuals | Compare prior call guidance to what was actually reported |
| Capex plans | Amount, timeline, funded how (debt/internal accruals) |
| New segments / products | Any pivot or expansion that changes the business mix |
| Order book | Size, executable timeline, client concentration |
| Margin commentary | Reasons given for compression or expansion |
| Debt commentary | Management narrative around debt levels and reduction plans |
| Red flags 🚩 | Defensive language, missed targets with excuses, promoter pledging mention, auditor change mention |
| Positives ✅ | Specific wins, new clients, export breakthrough, technology moat articulated |
| Outlook-changing plans | Acquisitions, demergers, large contracts, regulatory tailwinds/headwinds |

**Guidance vs Actuals Tracker** (build this table):
```
| Quarter | Metric | Guided | Actual | Met? |
|---------|--------|--------|--------|------|
| Q2FY25  | Revenue growth | 20% YoY | 7% YoY | ❌ Missed |
```
Consistent misses = 🚩. Consistent beats = ✅.

**Tone markers to watch:**
- Hedging language ("subject to market conditions", "we hope", "targeting") vs
  confident specifics ("we have visibility", "order book covers X quarters")
- Repeated deferrals of the same question across calls
- CFO/MD departure mentioned
- Auditor qualification mentioned even briefly

---

### Agent D — Annual Report Intelligence

**Source: BSE filings — category "Annual Report"**

Fetch the latest annual report PDF from BSE:
```
web_fetch https://www.bseindia.com/corporates/ann.html?scrip=<SCRIP_CODE>&Category=Annual%20Report&subcategory=-1
```

Annual reports are large (100–300+ pages). **Do not read end-to-end.**
Navigate directly to these sections:

**1. Auditor's Report (Standalone + Consolidated)**
- Any qualifications or emphasis of matter? → 🚩 if yes, quote exact language
- Auditor name and tenure — if auditor changed in last 3 years → 🚩 flag
- Key Audit Matters (KAMs) — what did auditors flag as high-risk areas?

**2. Related Party Transactions (RPT) — Notes to Accounts**
- Total RPT as % of revenue — if >10% and growing → 🚩
- Nature of transactions: sales to promoter entities, loans to subsidiaries,
  management fees, rent paid to promoter-owned entities
- Are RPTs at arm's length? Any auditor qualification on this?

**3. Director Report / Board Changes**
- Any independent director resignations in last 2 years? → 🚩 (especially if mid-term)
- Key managerial personnel changes (CEO, CFO, CS)
- Reasons given for departures — vague reasons = 🚩

**4. Litigation and Contingent Liabilities**
- Any material legal cases (tax disputes, regulatory action, customer disputes)?
- Contingent liabilities > 20% of net worth → flag the quantum

**5. Remuneration vs Profit**
- MD/CEO/Promoter remuneration trend vs PAT trend
- If remuneration rising while PAT flat/falling → 🚩
- Check remuneration as % of PAT — SEBI limit is 5% for profitable companies

**6. Promoter Loans**
- Any loans given by company to promoters or promoter entities?
- Inter-corporate deposits to related parties?
- These are classic red flags in Indian small/mid caps → 🚩 if found

**7. Accounting Policy Changes**
- Any change in depreciation method, revenue recognition, or inventory valuation?
- Year-on-year consistency check

---

### Agent E — News & Peers

**News (last 90 days):**
```
web_search "<COMPANY NAME> stock news site:economictimes.indiatimes.com OR site:moneycontrol.com OR site:business-standard.com"
web_search "<NSE_SYMBOL> NSE announcement block deal insider trading 2025"
```

Flag if found:
- 🚩 Promoter selling (especially >1% in a quarter)
- 🚩 Block deals by institutions (large exit)
- 🚩 Regulatory action (SEBI, GST, ED, IT dept)
- ✅ Large order wins / contract announcements
- ✅ Management interviews with specific forward-looking statements
- ✅ Institutional buying (FII/DII increases)
- Note any analyst initiations or target revisions (cite source)

**Peers (auto-select):**

Select 3–5 peers from the same NSE sector/industry. Prefer direct business model
comparables over index constituents.

Fetch peer data from NSE or Screener:
```
web_fetch https://www.screener.in/company/<PEER_SYMBOL>/consolidated/
```

Build comparison table:

| Company | Mkt Cap | P/E | EV/EBITDA | ROE | ROCE | D/E | Rev CAGR 3Y |
|---------|---------|-----|-----------|-----|------|-----|-------------|
| <TARGET>| | | | | | | |
| Peer 1  | | | | | | | |
| Peer 2  | | | | | | | |

Tag all peer data with source and date. Note if target company is premium/discount
to peers and on what basis (faster growth? better margins? cleaner balance sheet?).

---

## Phase 2 — Cross-Check & Synthesis

Run these consistency checks before writing the output:

| Check | Flag if |
|---|---|
| PAT vs Operating CF | OCF < 50% of PAT for 2+ consecutive years |
| Debt vs Revenue growth | Debt growing faster than revenue for 3Y |
| Guidance accuracy | >50% of tracked guidance points missed |
| RPT trend | RPT as % of revenue increasing YoY |
| Auditor tenure | Changed within last 3 years |
| Promoter holding | Declining > 2% per year |
| Capex vs Depreciation | If capex < depreciation for 3Y = no growth investment |
| Working capital | Receivables days increasing while revenue flat |

Each flag found in cross-checks must appear explicitly in the output under
"Cross-Check Findings".

---

## Output Format

Save as: `<SYMBOL>-research-<YYYY-MM-DD>.md`

```markdown
# <Company Name> (<SYMBOL>) — Fundamental Research
_Generated: <DD Mon YYYY> | Reporting Basis: Consolidated [or Standalone — flag if so]_
_Concall depth: <N> quarters | Annual report: FY<YY>_
_Sources: BSE Filings, NSE Data, Annual Report FY<YY>_

---

## ⚡ Quick Snapshot
| Metric | Value | Source |
|--------|-------|--------|
| CMP | ₹ | [NSE | date] |
| Market Cap | ₹ Cr | [NSE | date] |
| 52W High / Low | ₹ / ₹ | [NSE | date] |
| P/E (TTM) | x | [NSE | date] |
| P/B | x | [NSE | date] |
| Dividend Yield | % | [NSE | date] |
| Delivery % | % | [NSE | date] |
| Sector | | |
| F&O Listed | Yes/No | |

---

## 📊 10-Year Fundamental Trend
_[Data confidence: HIGH/MEDIUM — source noted per cell]_

[Revenue, PAT, EBITDA margin, ROE, ROCE, D/E, FCF table — 10 years]

**CAGR Summary:**
- Revenue: 3Y __% | 5Y __% | 10Y __%
- PAT: 3Y __% | 5Y __% | 10Y __%

---

## 💰 Debt & Cash Flow Analysis
[Narrative + numbers with source tags]

🚩 / ✅ flags as applicable

---

## 📞 Concall Intelligence (<N> quarters: Q<X>FY<YY> to Q<X>FY<YY>)

### Guidance vs Actuals Tracker
[Table]

### 🚩 Red Flags from Concalls
[Explicit list — each with the quarter it was found and exact source PDF URL]

### ✅ Positives from Concalls
[Explicit list — each with source]

### Outlook-Changing Plans
[Capex, new segments, acquisitions, order book visibility — with source]

---

## 📋 Annual Report — Governance Check (FY<YY>)
_[Source: BSE Filing <PDF URL> | <date>]_

### Auditor Findings
### Related Party Transactions
### Director & KMP Changes
### Litigation & Contingent Liabilities
### Remuneration vs Profit
### Promoter Loans / Inter-corporate Deposits
### Accounting Policy Changes

🚩 / ✅ flags as applicable

---

## 📰 News & Recent Developments (Last 90 Days)
[Bullet list — each with source URL and date]

🚩 / ✅ flags as applicable

---

## 🔄 Peer Comparison
[Table with source tags]

Brief qualitative note: where does the target company stand vs peers and why.

---

## ⚠️ Cross-Check Findings
[Each inconsistency found with the check name, what was found, and source]

---

## 🕳️ Data Gaps & Confidence Notes
[Everything that could not be fetched, with what was tried and what to verify manually]

_Disclaimer: This report is for research purposes only. It is not investment advice.
All data must be independently verified before making any financial decision._
```

---

## Failure Handling

| Failure | Action |
|---|---|
| NSE API blocked | Fallback to Moneycontrol quote page |
| BSE concall PDF 404 | Try NSE announcements; note gap in output |
| Screener.in blocked | Note `[Screener unavailable — paste CSV export for 10Y data]` |
| Annual report PDF too large to parse fully | Extract only the 7 target sections listed above |
| Peer data unavailable | Use web_search for peer metrics; lower confidence tag |
| Company has no concalls (small cap) | Note explicitly; rely more heavily on annual report |

---

## Reference Files

- `references/bse-endpoints.md` — Full BSE URL patterns, scrip code lookup,
  filing category codes, and curl templates with required headers
- `references/nse-endpoints.md` — NSE API endpoints, cookie negotiation pattern,
  and known failure modes
- `references/red-flag-playbook.md` — Expanded list of Indian market-specific
  red flags with historical case examples

Read a reference file only when you need it. They are not required for every run.
