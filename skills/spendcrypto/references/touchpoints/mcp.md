# Touchpoint: MCP

> Internal only — user hears plain shopping language, not tool or URL names.

**URL:** `https://api.spendcrypto.com/mcp` (Streamable HTTP)

## Auth

| Method | When |
| --- | --- |
| **OAuth** | Claude.ai, Grok custom connector — browser login + consent on first tool call |
| **API key** | Cursor, Claude Code — `Authorization: Api-Key YOUR_KEY` or `X-Api-Key` |

OAuth metadata: `GET https://api.spendcrypto.com/.well-known/oauth-authorization-server`

## Tools (10)

| Tool | Hint | Purpose |
| --- | --- | --- |
| search_products | read | Catalog search |
| get_product | read | Slug details |
| quote | read | Exact SCC/crypto price |
| get_order | read | Status; codes redacted |
| list_orders | read | History |
| get_account | read | Email + Spend Credits balance |
| get_esim_usage | read | Data usage |
| create_order | write | Place order — **confirm first** |
| cancel_order | write | Cancel unpaid |
| reveal_codes | write | Voucher / eSIM install data |

## Per-client setup

### Cursor — `.cursor/mcp.json`

```json
{
  "mcpServers": {
    "spendcrypto": {
      "url": "https://api.spendcrypto.com/mcp",
      "headers": { "Authorization": "Api-Key YOUR_KEY" }
    }
  }
}
```

Create keys at [spendcrypto.com/developers/keys](https://spendcrypto.com/developers/keys).

### Claude Code (plugin)

```bash
/plugin marketplace add spendcrypto/spendcrypto-agents
/plugin install spendcrypto@spendcrypto-skills
/reload-plugins
```

Or manual:

```bash
claude mcp add spendcrypto --url https://api.spendcrypto.com/mcp
```

OAuth runs on first tool call.

### Claude.ai

Settings → Connectors → Add custom connector → URL `https://api.spendcrypto.com/mcp`. Complete OAuth when prompted.

### Grok

[grok.com/connectors](https://grok.com/connectors) → Custom MCP → same URL. OAuth on first use.

See [grok.md](../harnesses/grok.md) for Grok Bot templates.

## create_order payments

- `payment_method=scc` — instant if Spend Credits cover the quote
- `payment_method=crypto` — returns `payment_url`; user pays on web; poll `get_order`

Full REST mirror: [api.md](api.md)
