# Getting access

SIWAI's API and MCP server are included with a paid SIWAI subscription
($99/month, or $990/year; see https://siwai.app/pricing). New accounts start with a
7-day free trial; a card is required to start it.

## Option 1: OAuth (Claude, ChatGPT and other OAuth-capable clients)

Add `https://siwai.app/api/mcp` as a remote / custom connector. The client discovers
SIWAI's OAuth server from the `401` response
(`WWW-Authenticate: Bearer realm="siwai", resource_metadata="https://siwai.app/.well-known/oauth-protected-resource"`),
registers itself (dynamic client registration), and sends you to
`https://siwai.app/oauth/authorize` to sign in and approve scopes. PKCE S256 is required.
OAuth needs an active paid subscription.

## Option 2: API key (Cursor, Claude Desktop, scripts)

1. Subscribe at https://siwai.app/pricing.
2. Open **Account settings → API keys**.
3. Name the key and tick the scopes you need, then create it.
4. Copy the raw key (it starts with `siwai_`). It is shown once; SIWAI stores only a hash.
5. Send it as `Authorization: Bearer siwai_...`.

Up to 10 keys per account. Keys can be revoked at any time from the same screen.

## Scopes

| Scope | Default | Covers |
|---|---|---|
| `market` | on | setups, confluence, outcomes, screener, funds, tickers, financials, news, calendars, profile updates |
| `accounts` | off | the key owner's IBKR / Hyperliquid snapshots (stats, positions, recent trades) |
| `mia` | off | ask MIA (separate, lower daily cap) |
| `workspace` | off | watchlist, feed filters, chart prefs |

## Daily limits (per key, UTC day)

| Plan | Requests / day | MIA / day |
|---|---|---|
| Starter | 200 | 5 |
| Pro | 1,000 | 20 |
| Premium | 5,000 | 50 |

Errors: `401` missing/invalid/revoked key, `403` missing scope or no active paid plan,
`404` unknown path, `429` daily cap reached.
