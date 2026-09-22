---
name: spendcrypto
description: "Buy gift cards and eSIMs on SpendCrypto — US/international catalog, prepaid Spend Credits (SCC), crypto payment links. MCP at api.spendcrypto.com with OAuth or API key. Triggers: SpendCrypto, gift card, eSIM, prepaid checkout, agent commerce."
compatibility: "Primary touchpoint: SpendCrypto MCP (OAuth on Claude/Grok, API key on Cursor/Claude Code). Fallback: REST /api/v1/ with Api-Key. Payment: SCC instant pay or crypto payment link."
metadata:
  author: spendcrypto
  version: "1.0.0"
  homepage: "https://spendcrypto.com/developers"
  docs: "https://spendcrypto.com/developers/api"
---

# SpendCrypto

Gift cards and eSIMs with the same catalog as spendcrypto.com. Agents buy on behalf of a signed-in user with **prepaid Spend Credits** or a **crypto payment link**.

## User-facing language

Concierge voice — never say MCP, OAuth, API key, JWT, endpoint, or tool names to the user.

**Say:** "I'll search for that gift card" · "Your total is … Spend Credits" · "Open the payment link to finish checkout" · "Your code is ready."

**Never say:** create_order, reveal_codes, SCC slug, idempotency, connector, harness.

| Internal | Say instead |
| --- | --- |
| quote | "The price is …" |
| create_order (scc) | "I'll place the order with your Spend Credits" |
| create_order (crypto) | "I'll send you a payment link" |
| reveal_codes | "Your code is ready" (deliver privately) |

**Flow:** search → quote → **confirm with the user** → create_order → pay if needed → get_order → reveal_codes. Never auto-buy.

Read [safeguards.md](references/safeguards.md) before any write tool.

## How to route

### 1. Pick touchpoint

| If | Read |
| --- | --- |
| MCP available (Claude, Grok, Cursor, Claude Code) | [mcp.md](references/touchpoints/mcp.md) |
| REST only (B2B script, no MCP) | [api.md](references/touchpoints/api.md) |

MCP URL: `https://api.spendcrypto.com/mcp`

### 2. Pick payment

| If | Read |
| --- | --- |
| User has Spend Credits on account | [scredit.md](references/wallets/scredit.md) — `payment_method=scc` |
| User will pay on-chain via link | [payment.md](references/wallets/payment.md) — `payment_method=crypto` |

Rank: **SCC first** (one step after confirm), then **crypto payment link** (user pays at spendcrypto.com/order/{sid}).

### 3. Host-specific setup

| Host | Read |
| --- | --- |
| Claude.ai / Claude Desktop | [claude-chat.md](references/harnesses/claude-chat.md) |
| Grok connectors / Grok Bot | [grok.md](references/harnesses/grok.md) |

## MCP tool flow (canonical)

1. `search_products` — query, country, product_type (`gift_card` | `esim` | `all`)
2. `get_product` — slug from search
3. `quote` — exact SCC and crypto totals; **read totals to the user**
4. User confirms product, amount, and payment method
5. `create_order` — `payment_method`: `scc` or `crypto`
6. `get_order` — poll until delivered (crypto: user pays at `payment_url` first)
7. `reveal_codes` — explicit second step; never paste codes in group chat or TTS

Write tools (`create_order`, `cancel_order`, `reveal_codes`) are never auto-approved.

## Account requirements

- **SCC:** SpendCrypto account + funded Spend Credits + MCP OAuth or API key
- **Crypto link:** Account optional for guest REST; MCP requires auth (OAuth or API key)
- API keys: [spendcrypto.com/developers/keys](https://spendcrypto.com/developers/keys)
- Fund credits: [spendcrypto.com/my-credits](https://spendcrypto.com/my-credits)

Human docs: [spendcrypto.com/developers](https://spendcrypto.com/developers)
