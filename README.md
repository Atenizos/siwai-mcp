<p align="center"><img src="logo.png" width="96" alt="SIWAI logo"></p>

# SIWAI MCP server

Remote MCP server for [SIWAI](https://siwai.app), a chart-pattern detection and technical
analysis platform. It gives AI agents read access to SIWAI's daily pattern scan, screener,
13F fund tracker, ticker fundamentals, news and economic / earnings / dividend calendars,
across stocks, crypto, indices, commodities and forex.

- **Endpoint:** `https://siwai.app/api/mcp`
- **Transport:** Streamable HTTP
- **Auth:** OAuth (PKCE S256, dynamic client registration) or `Authorization: Bearer siwai_...` API key
- **Registry name:** `io.github.Atenizos/siwai`
- **Docs:** https://siwai.app/docs/api · OpenAPI: https://siwai.app/api/v1/openapi.json

This repository holds the public listing metadata (`server.json`), docs and logo. The server
itself is hosted by SIWAI; there is nothing to install or run locally.

> Not financial advice. For informational purposes only. SIWAI finds setups; it does not
> place trades. The user still sizes the position, places the stop and takes the trade.

## What you can ask

- "Which breakout setups did SIWAI find on stocks today?"
- "Screen for stocks with ROE above 15%, P/E under 25 and a Breakout pattern."
- "What did the biggest tracked 13F funds buy or sell in NVDA last quarter?"
- "What high-impact economic events are on the calendar this week?"
- "Show me SIWAI's hit rate for Breakout + Impulse setups."

## Tools

24 tools; 23 are read-only and one (`update_watchlist`) replaces the user's watchlist.
See [docs/tools.md](docs/tools.md) for the full list with annotations and scopes.

## Access

The API and MCP server are included with a paid SIWAI subscription. See
[docs/api-key.md](docs/api-key.md) for OAuth, API keys, scopes and daily limits.

## Client setup

**Claude (claude.ai / Desktop), ChatGPT and other OAuth clients:** add a custom connector
with URL `https://siwai.app/api/mcp` and sign in when asked.

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=siwai&config=eyJ1cmwiOiJodHRwczovL3Npd2FpLmFwcC9hcGkvbWNwIn0=)

**Cursor** with an API key instead of OAuth (`.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "siwai": {
      "url": "https://siwai.app/api/mcp",
      "headers": { "Authorization": "Bearer siwai_YOUR_KEY" }
    }
  }
}
```

**Clients without remote-server support** (via `mcp-remote`):

```json
{
  "mcpServers": {
    "siwai": {
      "command": "npx",
      "args": ["mcp-remote", "https://siwai.app/api/mcp", "--header", "Authorization: Bearer siwai_YOUR_KEY"]
    }
  }
}
```

## Privacy and support

- Privacy policy: https://siwai.app/privacy
- Terms: https://siwai.app/terms
- Support: contact@siwai.app

## License

The contents of this repository (metadata and docs) are MIT licensed. The SIWAI service is
proprietary and subject to its [terms](https://siwai.app/terms).
