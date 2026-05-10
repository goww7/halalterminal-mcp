# Halal Terminal MCP — Shariah-compliant stock & ETF screening for AI agents

[![npm version](https://img.shields.io/npm/v/@halalterminal/mcp.svg)](https://www.npmjs.com/package/@halalterminal/mcp)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)
[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)

The official **Model Context Protocol** server for [Halal Terminal](https://halalterminal.com). Screen any stock or ETF for **Shariah (Islamic) compliance** across **5 methodologies** — AAOIFI, DJIM, FTSE, MSCI, S&P — audit portfolios, calculate **zakat** and **dividend purification**, and pull market data, news and SEC filings, all from inside any MCP-compatible AI agent: **Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose**, and more.

> *"Is AAPL halal?"* · *"Audit my portfolio: AAPL 30%, MSFT 20%, JNJ 50%"* · *"Calculate zakat on my holdings."*

## Install

```bash
# Recommended — npx (no install)
npx -y @halalterminal/mcp

# Or pin globally
npm install -g @halalterminal/mcp
```

Then **get a free API key** at [api.halalterminal.com](https://api.halalterminal.com) (email-only signup, no credit card) and follow [CONNECT.md](CONNECT.md) for your client.

### One-liner: Claude Desktop

```json
{
  "mcpServers": {
    "halalterminal": {
      "command": "npx",
      "args": ["-y", "@halalterminal/mcp"],
      "env": { "HALALTERMINAL_API_KEY": "ht_yourkey" }
    }
  }
}
```

### One-liner: Claude Code

```bash
claude mcp add --transport sse halalterminal \
  https://mcp.halalterminal.com/sse \
  --header "X-API-Key: ht_yourkey"
```

### One-liner: Cursor / Windsurf / direct SSE

```
https://mcp.halalterminal.com/sse?api_key=ht_yourkey
```

Full client guide: [CONNECT.md](CONNECT.md).

## What you get — 22 tools across 8 categories

| Category | Tools |
|---|---|
| **Screening** | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| **Market data** | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| **ETF analysis** | `get_etf_info`, `etf_purification`, `compare_etfs` |
| **Portfolio & watchlist** | `scan_portfolio`, `manage_watchlist` |
| **Comparison** | `compare_stocks` |
| **Income & zakat** | `get_dividends`, `calculate_zakat` |
| **News & filings** | `get_news`, `get_sec_filings` |
| **Reports & education** | `generate_report`, `islamic_finance_education` |

Full input/output reference in [TOOLS.md](TOOLS.md). End-to-end prompt walkthroughs in [EXAMPLES.md](EXAMPLES.md).

## Why Halal Terminal

- **5 methodologies, one tool.** AAOIFI, DJIM (Dow Jones Islamic Market), FTSE Shariah, MSCI Islamic, and S&P Shariah — each with its own business-activity rules and financial-ratio thresholds, surfaced side-by-side per stock.
- **Holdings-level ETF screening.** Every underlying constituent is screened, weighted, and aggregated to an overall verdict + a per-dollar purification rate. Works on SPY, QQQ, VTI, ISDU, SPUS, HLAL, and 8,000+ more.
- **Zakat & purification, computed.** 2.5% zakat against a live nisab threshold; impure-portion calculation per dividend based on the issuer's non-compliant revenue ratio.
- **Bulk index screens.** Trigger-and-poll runs on the S&P 500, NASDAQ-100, FTSE 100 and friends; filter results by methodology, sector, or compliant-only.
- **Free tier, no credit card.** Email signup → key in your inbox → ~5–10 full screens per month on the free plan.

## Endpoint & transport

```
SSE: https://mcp.halalterminal.com/sse
Auth: X-API-Key: <your_key>   (or ?api_key=<your_key>)
```

Transports supported: **SSE** (recommended), **stdio** (via this `@halalterminal/mcp` bridge for clients that need it).

## Plans & quotas

The Halal Terminal API is **token-metered**, not request-metered.

| Plan | Monthly tokens | Price | Notes |
|---|---|---|---|
| **Free** | 50 | $0 | ~5–10 full screenings · email signup, no credit card |
| **Starter** | 2,500 | $19 | Individual investors |
| **Pro** | 15,000 | $49 | Webhooks, bulk priority |
| **Enterprise** | Unlimited | $199+ | Custom methodologies, SLA |

Sign up: [api.halalterminal.com](https://api.halalterminal.com) · Pricing: [halalterminal.com/pricing](https://halalterminal.com/pricing)

## What this MCP server is NOT

- **Not a fatwa.** Every verdict is a methodology-based screening. Consult a qualified scholar for personal rulings.
- **Not a trading platform.** No broker integrations, no order execution.
- **Not a real-time alert system.** Request-response only in v1; webhook-driven alerts are on the Pro+ roadmap.
- **English-only in v1.** Arabic + French rendering is on the roadmap.

## FAQ

### Is this MCP server free to use?

Yes. The `@halalterminal/mcp` package is Apache-2.0 and free. The Halal Terminal API has a free tier (50 tokens / month, no credit card) that covers ~5–10 full stock screenings — enough to evaluate it before upgrading.

### Which AI clients does it work with?

Any client that supports the Model Context Protocol over **SSE** or **stdio** — Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose, and more. SSE is recommended; the `@halalterminal/mcp` package wraps it as stdio for clients that don't yet support SSE.

### How is "halal" determined?

Each verdict applies the published rules of the chosen methodology — **AAOIFI**, **Dow Jones Islamic Market (DJIM)**, **FTSE Shariah**, **MSCI Islamic**, and **S&P Shariah**. Two layers: (1) a **business-activity** screen (no alcohol, gambling, conventional finance, adult content, weapons, pork, …), then (2) **financial-ratio** thresholds (e.g. interest-bearing debt over market cap, illiquid assets, interest income share). The MCP exposes all five verdicts so the user — or scholar — can pick the standard they follow.

### What is dividend purification?

When you hold a stock with a small share of non-compliant revenue, scholars require donating the non-compliant fraction of any dividend received. `calculate_zakat(calculation_type="purification", …)` and `get_dividends(include_purification=True)` compute that amount automatically.

### Can it screen ETFs?

Yes — `screen_etf` walks every underlying holding, applies the methodology to each, and returns an overall verdict, compliant percentage, and aggregate purification rate. Sukuk ETFs are handled separately (asset-based methodologies).

### Can I screen an entire index at once?

Yes — `bulk_screen` triggers an asynchronous run on indices like S&P 500, NASDAQ-100, FTSE 100, and lets you poll for status, filter results by methodology / sector / compliant-only, and diff two runs.

### Does it support webhooks for compliance changes?

Webhooks are a Pro-plan feature on the API roadmap; v1 of this MCP is request-response only.

### Where do I report bugs or request tools?

[github.com/goww7/halalterminal-mcp/issues](https://github.com/goww7/halalterminal-mcp/issues) or email yassir@halalterminal.com.

## Related projects (sibling OSS)

Open-source tools that share the same Halal Terminal API — different surfaces, same data:

| Project | What it is | License |
|---|---|---|
| [**halalterminal-claude-skills**](https://github.com/goww7/halalterminal-claude-skills) | Claude Code plugin — curated skills, slash commands, and a portfolio-builder subagent on top of this MCP server. | Apache-2.0 |
| [**yassir-oss**](https://github.com/goww7/yassir-oss) | Open-source ReAct agent for halal finance research — CLI + web UI; supports OpenAI / Anthropic / local LLMs. | Apache-2.0 |
| [**halal-discord-bot**](https://github.com/goww7/halal-discord-bot) | Discord bot — `/halal AAPL`, `/portfolio`, `/trending` slash commands. | MIT |
| [**halal-portfolio-tracker**](https://github.com/goww7/halal-portfolio-tracker) | Next.js 14 app — enter holdings, get per-stock compliance + portfolio halal % + purification owed. One-click Vercel deploy. | MIT |
| [**halal-pine**](https://github.com/goww7/halal-pine) | TradingView Pine Script v5 indicator that overlays compliance status on charts. Refreshed daily from this API. | MIT |

## License & trademarks

Apache-2.0 — see [LICENSE](LICENSE).

"Halal Terminal", "HalalTerminal", and the Halal Terminal logo are reserved trademarks — see [TRADEMARKS.md](TRADEMARKS.md).

## Legal

- [Legal & Disclaimer](https://halalterminal.com/legal) — educational-research framing, investment disclaimer, Shariah compliance notice, liability limits, jurisdiction notices
- [Privacy Policy](https://halalterminal.com/privacy)
- [Cookie Policy](https://halalterminal.com/cookies)

## Support

- Contact: yassir@halalterminal.com
- Dashboard: [halalterminal.com/dashboard](https://halalterminal.com/dashboard)
- API docs: [api.halalterminal.com/docs](https://api.halalterminal.com/docs) (Swagger) · [api.halalterminal.com/redoc](https://api.halalterminal.com/redoc) (ReDoc)

---

Powered by Halal Terminal — [halalterminal.com](https://halalterminal.com)
