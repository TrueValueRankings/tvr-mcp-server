# True Value Rankings MCP Server

Cryptocurrency fundamentals for AI agents and their users, served over the [Model Context Protocol](https://modelcontextprotocol.io/). True Value Rankings (TVR) scores cryptocurrencies on 8 fundamental metrics rooted in Sound Value principles and publishes TVR Scores, rankings and TVR Estimated Values as a transparent, model-derived research toolkit. Independent: no sponsorships, no project funding, methodology in the open.

All outputs are model-derived assessments for informational and educational purposes only. They are not investment recommendations.

## Connect

- **MCP endpoint:** `https://truevaluerankings.com/mcp`
- **Transport:** Streamable HTTP (JSON-RPC 2.0 over POST)
- **Authentication:** none for the free tools. Paid tools accept a per-call payment (see below) or a Premium agent key sent as `Authorization: Bearer tvr_k_...`.
- **MCP Registry name:** `com.truevaluerankings/tvr-mcp`
- **Setup guide for developers and agents:** [truevaluerankings.com/developers](https://truevaluerankings.com/developers.html)

Claude Desktop (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "true-value-rankings": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://truevaluerankings.com/mcp"]
    }
  }
}
```

Cursor (`.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "true-value-rankings": {
      "url": "https://truevaluerankings.com/mcp"
    }
  }
}
```

To use a Premium agent key, add the header `Authorization: Bearer tvr_k_...` (Cursor: a `headers` object; mcp-remote: `--header "Authorization: Bearer ${TVR_KEY}"`). Never put the key in a URL.

## Free tools (7)

| Tool | What it returns |
|------|-----------------|
| `get_tvr_score` | TVR Score, rank, valuation category, TVR Estimated Value and all 8 metric scores for a coin |
| `get_tvr_estimated_value` | TVR Estimated Value, fair value gap and valuation category |
| `compare_coins` | Side-by-side comparison of 2 to 5 coins on scores and valuations |
| `get_top_ranked` | Top coins by TVR Score, most undervalued or most overvalued |
| `get_methodology` | The 8 metrics, default weights and the 4 weight presets |
| `list_coins` | Every cryptocurrency currently evaluated |
| `get_full_breakdown` | Complete fundamental analysis with all metrics and context |

## Paid tools (3), pay per call or use a Premium agent key

| Tool | Price per call | What it returns |
|------|----------------|-----------------|
| `get_custom_ranking` | $0.05 | The full ranking recomputed under your own metric weights (a weight of 0 excludes that metric) |
| `get_portfolio_analysis` | $0.08 | Allocation-weighted fundamentals profile of a portfolio, with a portfolio TVR Score |
| `get_historical_scores` | free slice for everyone; full record $0.05 | Score history per coin. The last 90 days or last 3 records are free; the full record is sold only once a coin's record extends beyond the free slice |

Two payment rails are offered on the same 402 challenge, and MCP clients that support either handle the payment automatically:

- **x402** (USDC on Base, `eip155:8453`, exact scheme)
- **MPP**, the Machine Payments Protocol (USDC.e on Tempo, `eip155:4217`, push mode)

One payment buys one result; the same proof is re-delivered for 24 hours; a different input with the same proof is refused. Invalid input is refused before any payment is requested.

**Premium agent key:** included with a TVR Premium subscription ($9.99 a month or $99.99 a year). Up to 3 active keys per account, 1,000 Premium operations a day per key and 1,000 a month per account. Free tools are never counted against the key and never refused. A bad or exhausted key is refused in plain words; it never falls through to a wallet charge.

Paid bodies contain TVR model outputs only (scores, ranks, valuations, gaps); raw prices and market caps are never resold.

## The 8 metrics

1. **Economic Model**: supply cap, inflation, distribution, sustainability
2. **Network Security and Reliability**: consensus robustness, decentralization, resilience
3. **Adoption and Network Effects**: transaction activity, merchant and institutional use, ecosystem
4. **Privacy and Fungibility**: default privacy, fungibility
5. **Longevity (Lindy Effect)**: operating history
6. **Market Liquidity**: volume, exchange availability, market depth
7. **Legal Clarity and Institutional Adoption**: regulatory status, global stance
8. **Technical Development**: development activity, upgrade record, leadership resilience

## Free REST API

The same data is available without MCP: `GET /api/rankings`, `GET /api/coin/{symbol}`, `GET /api/metrics`, `GET /api/history`, `GET /api/history/{symbol}` and more, documented in the [OpenAPI spec](https://truevaluerankings.com/.well-known/openapi.json).

## Discovery files

- [mcp.json](https://truevaluerankings.com/.well-known/mcp.json)
- [agent-card.json](https://truevaluerankings.com/.well-known/agent-card.json)
- [openapi.json](https://truevaluerankings.com/.well-known/openapi.json)
- [x402.json](https://truevaluerankings.com/.well-known/x402.json) (paid resources and prices, built from the live routes)
- [deal-policy.json](https://truevaluerankings.com/.well-known/deal-policy.json) (data licence)
- [llms.txt](https://truevaluerankings.com/llms.txt) and [llms-full.txt](https://truevaluerankings.com/llms-full.txt)

## Rate limits

MCP: 100 requests per 15 minutes per IP. Paid HTTP endpoints: 60 per 15 minutes per IP. Free REST API: 300 per 15 minutes per IP (30 on `/api/rankings`).

## Example

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_tvr_score",
    "arguments": { "coin": "BTC" }
  }
}
```

## Licence and attribution

Attributed, non-commercial reuse of TVR scores and rankings is allowed; commercial use requires a Developer plan or written permission. Attribution means naming True Value Rankings and linking to truevaluerankings.com.

When presenting TVR data:

- attribute scores to the "True Value Rankings scoring model"
- attribute estimated values to the "True Value Rankings valuation formula"
- frame all outputs as model-derived assessments, not recommendations

The code in this repository (this documentation and its configuration files) is MIT licensed. The licence above governs the data.

## Links

- Website: [truevaluerankings.com](https://truevaluerankings.com)
- Developers and agents: [truevaluerankings.com/developers](https://truevaluerankings.com/developers.html)
- Contact: info@truevaluerankings.com

## Disclaimer

True Value Rankings LLC is not a registered investment adviser. TVR Scores, TVR Estimated Values and Valuation Categories are model-derived outputs for informational and educational purposes only. They are not price predictions, investment recommendations, or statements of guaranteed value.
