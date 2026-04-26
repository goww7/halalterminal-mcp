# Tool reference

The Halal Terminal MCP server exposes **22 tools** organized into 8 functional groups. All tools return JSON-encoded strings.

> Authentication is enforced at the SSE transport layer — every tool call requires a valid `X-API-Key`.

## Screening

### `screen_stock(symbol: str)`
Screen a stock for Shariah (Islamic law) compliance. Returns business-activity screening, financial-ratio checks against 5 methodologies (AAOIFI, DJIM, FTSE, MSCI, S&P), purification rate, and key financial metrics.

Use when asked *"Is [stock] halal?"* or *"Is [stock] Shariah-compliant?"*.

### `get_screening_result(symbol: str)`
Get a **cached** screening result without triggering a new screening. Faster than `screen_stock` but may return stale data.

### `get_all_screening_results()`
List every stock that has been screened, sorted by most recent.

### `screen_etf(symbol: str, force_refresh: bool = False)`
Screen an ETF by analyzing every underlying holding. Returns per-holding compliance, overall verdict, compliant percentage, and aggregate purification rate.

### `bulk_screen(action: str, ...)`
Manage bulk screening of entire market indices (S&P 500, NASDAQ-100, FTSE-100, …). The `action` parameter dispatches to:

| Action | Required args | Purpose |
|---|---|---|
| `trigger` | `index_name` | Start screening an index |
| `status` | optional `run_id` | Status of a run (latest if omitted) |
| `list_runs` | — | List all runs |
| `results` | `run_id` | Paginated results, filterable by `compliant` / `methodology` / `sector` |
| `summary` | `run_id` | Aggregate stats for a run |
| `cancel` | `run_id` | Cancel a running screening |
| `compare` | `run_id="id1,id2"` | Diff two runs |
| `list_indices` | — | Available indices |

## Market data

### `get_quote(symbol?: str, symbols?: list[str])`
Real-time quote(s) — price, change, volume, market cap, P/E, dividend yield. Pass `symbols` for batch queries; `symbol` is ignored when `symbols` is provided.

### `get_stock_info(symbol: str, full: bool = False)`
Reference data for a stock. With `full=True`, also returns the latest quote and screening result in one response (slower but more complete).

### `get_price_history(symbol: str, period: str, interval: str)`
Historical OHLC data.

- `period` ∈ `1d, 5d, 1mo, 3mo, 6mo, 1y, 2y, 5y, 10y, max`
- `interval` ∈ `1m, 5m, 15m, 1h, 1d, 1wk, 1mo`

### `get_trending_stocks(limit: int = 10)`
Biggest movers — price, % change, volume. Returns up to 16 stocks.

### `search_stocks(query, asset_type?, sector?, country?, exchange?, limit?)`
Search the catalog by name, ticker fragment, sector, country, or exchange. `asset_type` ∈ `equities` (default), `etf`.

## ETF analysis

### `get_etf_info(symbol: str, data_type: str)`
ETF fund metadata or full holdings breakdown.

- `data_type="holdings"` — every underlying stock with weights
- `data_type="fund_info"` — expense ratio, total assets, inception date, etc.

### `etf_purification(symbol, investment_amount, dividend_income?)`
Compute the purification amount (donate the impure portion) for an ETF investment, based on its holdings-level compliance.

### `compare_etfs(symbols: list[str])`
Side-by-side comparison of 2–5 ETFs with compliance analysis and holdings-overlap detection.

## Portfolio & watchlist

### `scan_portfolio(symbols: list[str], force_refresh: bool = False)`
Screen up to **100** stocks at once. Returns per-stock compliance and an aggregate summary (compliant count, non-compliant count, average purification rate).

### `manage_watchlist(action, name?, watchlist_id?, symbol?, symbols?)`
CRUD on stock watchlists. `action` ∈ `create | list | get | add_symbol | remove_symbol | delete`.

## Comparison

### `compare_stocks(symbols: list[str])`
Compare 2–5 stocks side-by-side on Shariah compliance, financial ratios, market data, and metadata.

## Income & zakat

### `get_dividends(symbol: str, include_purification: bool = False)`
Dividend history. With `include_purification=True`, computes the purification amount per dividend based on the stock's non-compliant revenue ratio.

### `calculate_zakat(calculation_type, holdings, gold_price_per_gram?)`
Calculate obligatory charity (`zakat`) or impure income (`purification`) on stock holdings.

- `calculation_type="zakat"` → 2.5% of eligible wealth above the nisab threshold. `holdings` items: `{"symbol": "AAPL", "market_value": 10000}`
- `calculation_type="purification"` → impure dividend income. `holdings` items: `{"symbol": "AAPL", "dividend_income": 500}`
- `gold_price_per_gram` (USD, default `65.0`) — used only for the zakat nisab threshold.

## News & filings

### `get_news(symbol?, source?, category?, query?, page?, limit?)`
Financial and Islamic-finance news. Stock-specific when `symbol` is set; otherwise the general feed with optional filters. Articles include title, source, date, URL, relevance metadata.

### `get_sec_filings(symbol, data_type, filing_type?, limit?)`
SEC EDGAR data for US-listed companies.

- `data_type="filings"` — filing history (10-K, 10-Q, 8-K, …); use `filing_type` to filter
- `data_type="facts"` — structured XBRL data (revenue, assets, …)

## Reports & education

### `generate_report(report_type, symbol?, symbols?)`
Detailed Shariah screening report.

- `report_type="screening"` — single-stock deep dive (requires `symbol`)
- `report_type="portfolio"` — multi-stock portfolio compliance (requires `symbols`)

### `islamic_finance_education(topic, query?, methodology_name?)`
Educational content. `topic` ∈:

- `glossary` — Islamic finance terms dictionary; filter with `query`
- `methodologies` — overview of all 5 Shariah screening methodologies
- `methodology_detail` — deep dive into one methodology (requires `methodology_name`)
- `screening_criteria` — financial ratio thresholds
- `purification_guide` — how to purify investment income
