# SIWAI MCP tools

Server: `https://siwai.app/api/mcp` (Streamable HTTP, server name `siwai`, version 1.5.0).
Every tool sets `title`, `readOnlyHint` and `destructiveHint`. Every JSON result includes
`"disclaimer": "Not financial advice. For informational purposes only."`

The server also exposes one resource: `siwai://openapi.json` (the SIWAI OpenAPI 3 spec, also at
https://siwai.app/api/v1/openapi.json).

| Tool | Title | Scope | Read-only | What it returns |
|---|---|---|---|---|
| `get_today_setups` | Today's setups | market | yes | Setups from the latest daily scan. Filters: market, pattern, timeframe, since, include_confluence, limit, offset. |
| `get_confluence` | Confluence setups | market | yes | Combined patterns (for example Breakout + Impulse) from the latest scan. |
| `get_setups` | Setups by ticker | market | yes | Current setups for one ticker. |
| `get_setup_outcomes` | Pattern outcomes | market | yes | Hit/fail summaries per pattern type. No candle series. |
| `get_setup_stats` | Public pattern stats | market | yes | Cached hit-rate summaries for Breakout and Breakout + Impulse. |
| `list_patterns` | Pattern catalog | market | yes | Every pattern type, including confluence combinations. |
| `list_screener_filters` | Screener filters | market | yes | Every screener filter with its type and allowed values. |
| `run_screener` | Run screener | market | yes | Tickers matching fundamental, technical and pattern filters. |
| `search_funds` | Search funds | market | yes | Tracked 13F funds by name, manager or holding ticker. |
| `get_fund_holdings` | Fund holdings | market | yes | Current holdings of one tracked fund (paginated). |
| `get_fund_activity` | Fund activity | market | yes | Buys, adds, reductions and sells of one fund vs the prior quarter. |
| `get_ticker` | Ticker snapshot | market | yes | Fundamentals, valuation and current setups for a ticker. |
| `get_ticker_financials` | Financial summaries | market | yes | Derived income, balance-sheet and cash-flow summaries. |
| `get_ticker_funds` | Funds for ticker | market | yes | Tracked funds that hold or recently changed a ticker. |
| `get_news` | Market news | market | yes | News tagged against the ticker universe. |
| `get_economic_calendar` | Economic calendar | market | yes | Economic events, filterable by date, country and impact. |
| `get_earnings_calendar` | Earnings calendar | market | yes | Upcoming earnings (default: next 7 days). |
| `get_dividends_calendar` | Dividends calendar | market | yes | Upcoming dividends (default: next 7 days). |
| `get_profile_updates` | Profile updates | market | yes | The SIWAI product changelog, newest first. |
| `list_accounts` | Connected accounts | accounts | yes | The key owner's IBKR and Hyperliquid snapshots. Never returns credentials. |
| `get_account_stats` | Account snapshot | accounts | yes | Stats, open positions and recent trades for IBKR or HYPERLIQUID. |
| `get_watchlist` | Watchlist | workspace | yes | The key owner's watchlist. |
| `update_watchlist` | Replace watchlist | workspace | **no** (`destructiveHint: true`, `idempotentHint: true`) | Replaces the key owner's watchlist with the list sent. |
| `ask_mia` | Ask MIA | mia | yes | An answer from MIA, SIWAI's assistant, built on SIWAI setups, screener, funds, news, financials and outcomes. Separate daily cap. |

No tool places trades, moves money or returns broker credentials. Trading stays in the SIWAI app.
Raw OHLC / candle feeds are never returned.
