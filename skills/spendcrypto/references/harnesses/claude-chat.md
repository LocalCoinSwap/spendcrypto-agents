# Harness: Claude.ai / Claude Desktop

## Connector setup

1. Open Claude → Settings → Connectors (or Desktop → Settings → Connectors)
2. Add custom MCP server
3. URL: `https://api.spendcrypto.com/mcp`
4. Save — on first tool use, complete SpendCrypto OAuth (email OTP + consent)

No API key in the connector config for Claude.ai — OAuth only.

## Plugin path (Claude Code)

```bash
/plugin marketplace add spendcrypto/spendcrypto-agents
/plugin install spendcrypto@spendcrypto-skills
/reload-plugins
```

Bundled `.mcp.json` points at the same URL; OAuth on first call.

## User experience

User asks to buy a gift card → agent searches and quotes → asks to confirm → places order with SCC or sends payment link → reveals code privately.
