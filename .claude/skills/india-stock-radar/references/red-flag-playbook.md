# Red Flag Playbook — Indian Equities

A reference for identifying and contextualising red flags specific to Indian listed
companies. Use this when evaluating concall transcripts, annual reports, and
financial trends.

---

## Category 1 — Accounting & Earnings Quality

### OCF vs PAT Divergence
**What:** PAT growing but Operating Cash Flow flat or negative for 2+ years
**Why it matters:** Profit can be manipulated through accruals; cash cannot.
Persistent divergence suggests aggressive revenue recognition or capitalization
of expenses.
**Where to check:** Cash Flow Statement — compare "Cash from Operations" vs
reported PAT over 5 years.
**Threshold:** OCF/PAT ratio < 0.6 for 2+ consecutive years → 🚩

### Revenue Recognition Timing
**What:** Revenue booked before cash/goods delivered (channel stuffing)
**Signs:** Receivable days rising faster than revenue growth; debtors > 90 days
increasing as % of total debtors.
**Where to check:** Notes to accounts — debtors aging schedule.

### Capitalisation of Expenses
**What:** Regular operating expenses being capitalized as assets (boosting profit)
**Signs:** Intangibles or CWIP growing faster than fixed assets; depreciation/
amortization suddenly changing.
**Where to check:** Fixed asset schedule in annual report notes.

### Inventory Build-up
**What:** Inventory days rising while revenue is flat or falling
**Why it matters:** Could indicate slow-moving or obsolete stock being carried
at inflated values.
**Threshold:** Inventory days up >20% YoY with flat revenue → flag

---

## Category 2 — Debt & Capital Allocation

### Debt Growing Faster Than Revenue
**Threshold:** Debt CAGR > Revenue CAGR over 3 years → 🚩
**Context:** Some is acceptable for capex-heavy businesses; flag if going to
working capital or acquisitions that haven't generated returns.

### Interest Coverage Erosion
**Threshold:** Interest coverage falling below 2x → 🚩; below 1x → 🚩🚩
**Where to check:** P&L — EBIT / Interest expense

### Promoter Pledging
**What:** Promoters pledging shares as collateral for personal/company loans
**Why it matters:** If share price falls, forced selling can create a death spiral.
**Where to check:** BSE shareholding pattern filing — "Shares pledged" column.
**Threshold:** Pledging > 20% of promoter holding → 🚩; rising over multiple
quarters → 🚩🚩

### Serial Acquirer with Poor Returns
**What:** Company making multiple acquisitions but consolidated ROE/ROCE declining
**Signs:** Goodwill on balance sheet rising; ROCE declining despite revenue growth.

---

## Category 3 — Governance & Promoter Behaviour

### Independent Director Resignation (Mid-Term)
**Why it matters:** IDs who resign early often cite inability to function independently
or governance concerns — they rarely say this explicitly but the timing signals it.
**Threshold:** Any mid-term resignation without clear reason → 🚩
**Especially concerning:** Resignation of audit committee chair or independent director
with finance background.

### Auditor Change
**Normal:** Big 4 to Big 4, or after 10-year mandatory rotation.
**Red flag:** Switching from a reputable auditor to a lesser-known firm,
especially during a period of stress or investigation → 🚩
**Threshold:** Auditor changed within last 3 years → flag; changed more than once
in 5 years → 🚩🚩

### Auditor Qualifications
**What:** Auditor unable to confirm specific balances or expresses doubt on
going concern.
**Why it matters:** Auditors are conservative — if they qualify, the underlying
issue is usually significant.
**Any qualification or emphasis of matter → 🚩; going concern doubt → 🚩🚩**

### Related Party Transactions (RPTs)
**Acceptable:** Sales to group companies at market rates with board/shareholder approval.
**Red flags:**
- Loans to promoter entities (company money going to promoters) → 🚩🚩
- Management fees / brand royalties paid to promoter-owned entities
- Rent paid to promoter-owned property at above-market rates
- RPT % of revenue rising year on year
**Threshold:** RPT > 10% of revenue and growing → 🚩

### Promoter Remuneration vs PAT
**SEBI limit:** 5% of net profit for profitable companies (11% if 2+ WTDs)
**Red flag beyond SEBI limits:** Promoter compensation rising while PAT is flat
or falling → 🚩
**Classic pattern:** Revenue grows, PAT stagnates, but promoter salary doubles.

### Promoter Holding Decline
**Context:** Some decline is natural (QIPs, ESOPs). Consistent decline is different.
**Threshold:** Promoter holding down > 2% per year for 3 consecutive years → 🚩
**Especially concerning if:** Decline accelerates during period of strong stock price
(promoters selling into strength).

---

## Category 4 — Concall-Specific Red Flags

### Guidance Misses (Repeated)
**Pattern:** Management guides X, delivers 0.5X, explains with macro/weather/
one-time reasons, then guides X again next quarter.
**Threshold:** >50% of tracked guidance points missed across last 4 quarters → 🚩

### Defensive or Evasive Language
Specific phrases that are historically associated with deteriorating situations:
- "We remain cautiously optimistic" (almost always negative)
- "The business is going through a temporary phase"
- "We will provide more clarity next quarter" (used repeatedly)
- "We don't comment on that" (for direct financial questions)
- "The numbers will speak for themselves" (when they haven't)

### Not Holding Concalls
**What:** Company stops conducting concalls or investor days
**Why it matters:** Usually precedes a negative announcement.
**Check:** If last concall was > 2 quarters ago for a mid/large cap → 🚩

### CFO Change Before Results
**Pattern:** CFO resigns or is replaced 1–2 quarters before a major negative event.
**Historical precedent:** This has preceded accounting irregularities in several
Indian cases.

---

## Category 5 — Sector-Specific Watchlist

### Infrastructure / Capital Goods
- Watch: Order book concentration (1 client > 30% = risk)
- Watch: Fixed-price contracts with no escalation clause in inflationary environment
- Watch: Debtors > 180 days in government contracts (classic cash flow trap)

### Pharma / Specialty Chemicals
- Watch: USFDA observations / warning letters → 🚩
- Watch: API price volatility impact on margins without pass-through ability
- Watch: Concentration in one geography (US generics cliff risk)

### Real Estate
- Watch: Collections vs bookings divergence
- Watch: Inventory overhang (unsold units > 3 years supply)
- Watch: Land bank on books at historic cost (may overstate or understate NAV)

### NBFCs / Lending
- Watch: GNPA and NNPA trend
- Watch: Capital adequacy ratio trajectory
- Watch: Concentration risk in loan book (sector or geography)
- Watch: ALM mismatch (short-term borrowing, long-term lending)

### Retail / Consumer
- Watch: Same-store sales growth vs total revenue growth divergence
- Watch: Inventory days increasing
- Watch: Gross margin compression without explanation

---

## Positive Signal Playbook (✅)

- FCF positive and growing for 5+ years — business generates real cash
- D/E declining while growth is strong — self-funded expansion
- Promoter increasing stake in open market (not ESOPs) — skin in the game
- Consistent dividend growth — management confidence in future cash flows
- ROE > 20% without high leverage — genuinely capital-efficient business
- Auditor unchanged for 5+ years (reputable firm) — stability and trust
- Management guidance consistently met or beaten — credible team
- Working capital days stable or improving during growth — operational discipline
- New large client or export market announcement with specifics — not vague
- Capex funded from internal accruals, not debt — financial prudence
