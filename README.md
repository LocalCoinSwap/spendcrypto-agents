# SpendCrypto Agents

Agent skills and MCP wiring for [SpendCrypto](https://spendcrypto.com) — gift cards and eSIMs with prepaid Spend Credits or crypto payment links.

## Quick start

### Claude Code

```bash
/plugin marketplace add spendcrypto/spendcrypto-agents
/plugin install spendcrypto@spendcrypto-skills
/reload-plugins
```

### Cursor

`.cursor/mcp.json`:

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

Keys: [spendcrypto.com/developers/keys](https://spendcrypto.com/developers/keys)

### Claude.ai / Grok

Add custom MCP connector → `https://api.spendcrypto.com/mcp` → OAuth on first use.

Human docs: [spendcrypto.com/developers](https://spendcrypto.com/developers)

## Repository layout

```
.claude-plugin/     Plugin manifest + marketplace
.mcp.json             Bundled MCP server URL
skills/spendcrypto/   Agent skill + references
```

## Skill

Primary skill: `skills/spendcrypto/SKILL.md`

Payment order: **Spend Credits (SCC)** first, then **crypto payment link**.

## Local validation

```bash
claude --plugin-dir ./
claude plugin validate .
```

## License

MIT — see [LICENSE](LICENSE)
