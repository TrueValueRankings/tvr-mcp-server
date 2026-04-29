# True Value Rankings MCP Server

Cryptocurrency fundamental analysis tools via the [Model Context Protocol](https://modelcontextprotocol.io/). Provides educational scoring and valuation data to help users conduct their own research using Sound Value principles.

## What This Server Does

TVR's scoring model evaluates cryptocurrencies across 8 fundamental metrics, producing:

- **TVR Scores** (0-100) measuring fundamental strength
- **TVR Estimated Values** (fair value estimates)
- **Valuation Categories** (Undervalued, Fair Value, Overvalued)

All outputs are model-derived assessments for informational and educational purposes only. They are not investment recommendations.

## Connect

**MCP Endpoint:** `https://truevaluerankings.com/mcp`

**Transport:** Streamable HTTP (POST)

**Discovery Files:**
- [mcp.json](https://truevaluerankings.com/.well-known/mcp.json)
- [agent-card.json](https://truevaluerankings.com/.well-known/agent-card.json)
- [openapi.json](https://truevaluerankings.com/.well-known/openapi.json)

**MCP Registry:** `com.truevaluerankings/tvr-mcp` v2.0.0

## Free Tools (6)

| Tool | Description |
|------|-------------|
| `get_tvr_score` | TVR Score, rank, valuation category, and strongest/weakest metrics for a cryptocurrency |
| `get_tvr_estimated_value` | Fair value estimate, fair value gap, and valuation category |
| `compare_coins` | Side-by-side comparison of 2-5 cryptocurrencies on scores and valuations |
| `get_top_ranked` | Top N coins by TVR Score, most undervalued, or most overvalued |
| `get_methodology` | Scoring methodology: 8 metrics, weights, descriptions, and weight presets |
| `list_coins` | All cryptocurrencies currently evaluated by TVR |

## Premium Tools (5)

Premium tools require micropayment via [x402](https://www.x402.org/) (pathUSD on Tempo mainnet). x402-compatible clients handle payment automatically.

| Tool | Price | Description |
|------|-------|-------------|
| `get_full_breakdown` | $0.03 | Complete fundamental analysis with all 8 metric scores and explanations |
| `get_historical_scores` | $0.03 | Score change history with dates and reasons |
| `get_custom_ranking` | $0.05 | Recalculate rankings with custom metric weights |
| `get_portfolio_analysis` | $0.08 | Fundamental strength analysis of a multi-coin portfolio |
| `get_comparison_report` | $0.05 | Detailed metric-by-metric comparison with analysis |

## The 8 Metrics

1. **Economic Model** - Supply cap, inflation, distribution, sustainability
2. **Network Security and Reliability** - Consensus robustness, decentralization, resilience
3. **Adoption and Network Effects** - Transaction activity, merchant/institutional use, ecosystem
4. **Privacy and Fungibility** - Default privacy, fungibility
5. **Longevity (Lindy Effect)** - Operating history
6. **Market Liquidity** - Volume, exchange availability, market depth
7. **Legal Clarity and Institutional Adoption** - Regulatory status, global stance
8. **Technical Development** - Dev activity, upgrade record, leadership resilience

## Rate Limits

100 requests per 15 minutes per IP address. Health checks are exempt.

## Example Usage

Send a JSON-RPC 2.0 POST request to the MCP endpoint:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "get_tvr_score",
    "arguments": {
      "coin": "BTC"
    }
  }
}
```

## Attribution

When presenting TVR data, please:
- Attribute scores to "True Value Rankings scoring model"
- Attribute estimated values to "True Value Rankings valuation formula"
- Frame all outputs as model-derived assessments, not recommendations

## Links

- **Website:** [truevaluerankings.com](https://truevaluerankings.com)
- **llms.txt:** [truevaluerankings.com/llms.txt](https://truevaluerankings.com/llms.txt)
- **Contact:** info@truevaluerankings.com

## Disclaimer

True Value Rankings LLC is not a registered investment adviser. TVR Scores, TVR Estimated Values, and Valuation Categories are model-derived outputs for informational and educational purposes only. They are not price predictions, investment recommendations, or statements of guaranteed value.
