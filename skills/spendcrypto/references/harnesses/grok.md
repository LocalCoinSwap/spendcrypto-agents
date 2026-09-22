# Harness: Grok

## Custom MCP connector

1. Go to [grok.com/connectors](https://grok.com/connectors)
2. Add custom MCP
3. URL: `https://api.spendcrypto.com/mcp`
4. OAuth on first tool invocation (SpendCrypto email OTP)

## Grok Bot (optional)

For a branded bot that only does gift cards:

- System prompt: concierge shopping — search, quote, confirm, buy with Spend Credits or payment link, reveal codes privately
- Attach the SpendCrypto MCP connector
- Do not expose tool names in bot copy
