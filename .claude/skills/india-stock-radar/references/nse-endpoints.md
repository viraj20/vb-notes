# NSE India — Endpoints & Cookie Pattern

## Critical: Cookie Negotiation

NSE blocks direct API calls without a prior session cookie. Always do this first:

```bash
# Step 1: Hit homepage to get cookies
curl -s -c /tmp/nse_cookies.txt \
  -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36" \
  https://www.nseindia.com/ > /dev/null

# Step 2: Now call the API with saved cookies
curl -s -b /tmp/nse_cookies.txt \
  -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36" \
  -H "Accept: application/json, text/plain, */*" \
  -H "Referer: https://www.nseindia.com/" \
  "https://www.nseindia.com/api/quote-equity?symbol=TCS"
```

If using web_fetch instead of bash, fetch the homepage first, then the API endpoint
in the same session. If this fails, fall back to BSE data or Moneycontrol.

---

## Key Endpoints

### Equity Quote (Price, P/E, Market Cap)
```
GET https://www.nseindia.com/api/quote-equity?symbol=<SYMBOL>
```
Returns: lastPrice, change, pChange, totalTradedVolume, totalTradedValue,
52weekHigh, 52weekLow, nearWKH, nearWKL, pe, pb, eps, bookValue, faceValue,
industry, symbol, companyName, isin

### Delivery Data
```
GET https://www.nseindia.com/api/quote-equity?symbol=<SYMBOL>&section=trade_info
```
Returns delivery volume and delivery percentage

### Shareholding Pattern
```
GET https://www.nseindia.com/api/corporate-shareholding-pattern?symbol=<SYMBOL>&series=EQ&from=<DD-MM-YYYY>&to=<DD-MM-YYYY>
```

### Financial Results (Corporate Filings)
```
GET https://www.nseindia.com/api/corporations?index=equities&symbol=<SYMBOL>
```

### Corporate Announcements
```
GET https://www.nseindia.com/api/corporate-announcements?index=equities&symbol=<SYMBOL>&from_date=<DD-MM-YYYY>&to_date=<DD-MM-YYYY>
```

### Annual Reports (NSE listing)
```
GET https://www.nseindia.com/api/annual-reports?index=equities&symbol=<SYMBOL>
```
Returns list of annual report PDFs with direct download links.

---

## Symbol Format Notes

- Always UPPERCASE: `TCS` not `tcs`
- Use NSE symbol not company name: `HDFCBANK` not `HDFC Bank`
- For series EQ (equity), most symbols work directly
- SME companies may not be available on NSE endpoints — fall back to BSE

---

## Moneycontrol Fallback (if NSE blocked)

Quote page pattern:
```
https://www.moneycontrol.com/india/stockpricequote/<sector-slug>/<company-slug>/<MC_CODE>
```

Example: `https://www.moneycontrol.com/india/stockpricequote/computers-software/tata-consultancy-services/TCS`

MC_CODE is their internal code — use web_search to find it:
```
web_search "moneycontrol <COMPANY NAME> stock price"
```

---

## Known Failure Modes

- NSE adds Akamai bot protection intermittently — if cookie negotiation fails,
  wait and retry once, then fall back to BSE price data
- The `quote-equity` endpoint sometimes returns 401 during market hours under load —
  retry after 5s
- Symbol lookup: if unsure of exact NSE symbol, use:
  `https://www.nseindia.com/api/search/autocomplete?q=<PARTIAL_NAME>`
