# Halal Terminal MCP

[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)

The official **Model Context Protocol** server for [Halal Terminal](https://halalterminal.com) — Shariah-compliant investing capabilities for AI agents.

Screen stocks and ETFs across **5 methodologies** (AAOIFI, DJIM, FTSE, MSCI, S&P), audit portfolios, calculate zakat and dividend purification, fetch market data, news, and SEC filings — directly from any MCP-compatible client (Claude Desktop, Claude Code, Cursor, Windsurf, …).

## What you get

**22 tools across 8 categories:**

| Category | Tools |
|---|---|
| Screening | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| Market data | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| ETF analysis | `get_etf_info`, `etf_purification`, `compare_etfs` |
| Portfolio & watchlist | `scan_portfolio`, `manage_watchlist` |
| Comparison | `compare_stocks` |
| Income & zakat | `get_dividends`, `calculate_zakat` |
| News & filings | `get_news`, `get_sec_filings` |
| Reports & education | `generate_report`, `islamic_finance_education` |

See [TOOLS.md](TOOLS.md) for full input/output reference.

## Quick start

1. **Get a free API key** at https://api.halalterminal.com (email → key in your inbox, no credit card).
2. **Connect your MCP client** — see [CONNECT.md](CONNECT.md) for Claude Desktop, Claude Code, Cursor, Windsurf, and direct SSE.
3. **Ask** your assistant — *"Is AAPL halal?"*, *"Audit my portfolio: AAPL 30%, MSFT 20%, JNJ 50%"*, *"Calculate zakat on my holdings."*

For end-to-end examples, see [EXAMPLES.md](EXAMPLES.md).

## Endpoint

```
https://mcp.halalterminal.com/sse
```

- Transport: **SSE** (Server-Sent Events). A stdio bridge snippet is provided in [CONNECT.md](CONNECT.md) for clients that require stdio.
- Auth: `X-API-Key: <your_key>` header (or `?api_key=<your_key>` query param).
- Rate limits: per-plan token quotas, see below.

## Plans and quotas

The Halal Terminal API is token-metered.

| Plan | Monthly tokens | Price | Note |
|---|---|---|---|
| Free | 50 | $0 | ~5–10 full screenings |
| Starter | 2,500 | $19 | for individual investors |
| Pro | 15,000 | $49 | webhooks, bulk priority |
| Enterprise | Unlimited | $199+ | custom methodologies, SLA |

Sign up: https://api.halalterminal.com

## What this MCP server is NOT

- **Not a fatwa.** Every verdict is a methodology-based screening. Consult a qualified scholar for personal rulings.
- **Not a trading platform.** No broker integrations, no order execution.
- **Not a real-time alert system.** Request-response only in v1 (webhooks coming in v2 for Pro+ users).
- **Not a multi-language tool.** English responses only in v1.

## Related projects

- **[halalterminal-claude-skills](https://github.com/goww7/halalterminal-claude-skills)** — Claude Code plugin with curated skills, slash commands, and a portfolio-builder subagent that wraps this MCP server with task-specific guidance.

## License

Apache-2.0 — see [LICENSE](LICENSE).

"Halal Terminal", "HalalTerminal", and the Halal Terminal logo are reserved trademarks — see [TRADEMARKS.md](TRADEMARKS.md).

## Legal

- [Legal & Disclaimer](https://halalterminal.com/legal) — educational-research framing, investment disclaimer, Shariah compliance notice, liability limits, jurisdiction notices
- [Privacy Policy](https://halalterminal.com/privacy)
- [Cookie Policy](https://halalterminal.com/cookies)

## Support

- Contact: yassir@halalterminal.com
- Dashboard: https://halalterminal.com/dashboard
- API docs: https://api.halalterminal.com/docs (Swagger) · https://api.halalterminal.com/redoc (ReDoc)

---

Powered by Halal Terminal — https://halalterminal.com
