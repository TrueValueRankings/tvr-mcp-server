---
name: true-value-rankings
description: Score, compare and rank cryptocurrencies on eight fundamental metrics with True Value Rankings (TVR). Use when someone asks how a coin scores on fundamentals, wants coins compared side by side, wants coins ranked under their own priorities, wants a portfolio profiled on fundamentals, or needs TVR's dated and hashed score history. Free MCP tools and a free JSON API; three paid results are bought one call at a time with x402 or MPP.
---

# True Value Rankings

True Value Rankings (TVR) scores cryptocurrencies on eight fundamental metrics: economic model, network security, adoption, privacy, longevity, liquidity, legal clarity and technical development. It publishes a TVR Score (0 to 100), a valuation category and a TVR Estimated Value for every covered coin. All outputs are model-derived educational information, not investment advice.

## Connect

- MCP, Streamable HTTP, no key: `https://truevaluerankings.com/mcp`
- Free JSON API, no key: `GET https://truevaluerankings.com/api/rankings`, `/api/coin/{symbol}`, `/api/metrics`, `/api/history/{symbol}`
- OpenAPI: `https://truevaluerankings.com/.well-known/openapi.json`
- x402 offer: `https://truevaluerankings.com/.well-known/x402.json`

## Which tool to use

| The person wants | Tool | Cost |
|---|---|---|
| How one coin scores, and why | `get_tvr_score`, then `get_full_breakdown` | free |
| Two to five coins side by side | `compare_coins` | free |
| The strongest coins, or the largest fair value gaps | `get_top_ranked` | free |
| How the scores are built | `get_methodology` | free |
| Which coins are covered | `list_coins` | free |
| How a coin's scores changed over time | `get_historical_scores` | free slice |
| Coins ranked under their own priorities | `get_custom_ranking` with `weights` (and optional `coins`) | $0.05 |
| A portfolio profiled on fundamentals | `get_portfolio_analysis` with `portfolio: [{coin, allocation}]` | $0.08 |
| The full score history of a coin | `get_historical_scores` with `scope: "full"` | $0.05, only once the record extends beyond the free slice |

Free answers from `compare_coins`, `get_top_ranked` and `get_full_breakdown` include a `paid_option` field naming the paid call that goes further, with its price and an example.

## Paying for one result

An unpaid call to a paid tool returns the offer and charges nothing. Over MCP the offer is a tool result with `isError`: the x402 `PaymentRequired` is in `structuredContent` and the MPP challenge list in `_meta["org.paymentauth/payment-required"]`. Pay and retry the same call with `_meta["x402/payment"]` (x402 version 2, USDC on Base, `eip155:8453`) or `_meta["org.paymentauth/credential"]` (MPP, USDC.e on Tempo, `eip155:4217`). Over HTTP the same products answer `402` with a `PAYMENT-REQUIRED` header and a `WWW-Authenticate: Payment` challenge. Invalid input is refused before any price is quoted. One payment buys one result; a lost response is delivered again on the same proof for 24 hours.

If the client has no wallet, show the person the price and stop. Never pay without the person's authorisation.

## Example: a watchlist under the person's priorities

1. `compare_coins` with `{"coins": ["BTC", "ETH", "XMR"]}` (free)
2. `get_custom_ranking` with `{"weights": {"economic_model": 30, "privacy": 25}, "coins": ["BTC", "ETH", "XMR"]}`: the first answer is the $0.05 offer; a wallet client pays it and receives the ranking. Missing weights take TVR's defaults.

## Rules

- Present every score as model-derived. Attribute scores to the True Value Rankings scoring model and estimated values to the True Value Rankings valuation formula, and link to truevaluerankings.com.
- Licence: Attributed, non-commercial reuse of TVR scores and rankings is allowed; commercial use requires a Developer plan or written permission. Attribution means naming True Value Rankings and linking to truevaluerankings.com.
- Commercial use (inside a product or service) needs the Developer plan: https://truevaluerankings.com/developers.html#developer-plan
- A coin TVR does not cover is answered with the list of covered coins; do not guess a score.
- Rate limits per IP: MCP 100 requests per 15 minutes, paid HTTP endpoints 60, free JSON API 300 (of which at most 30 to `/api/rankings`). Prefer the MCP tools for repeated questions.
