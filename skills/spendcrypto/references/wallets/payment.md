# Wallet: Crypto payment link

Fallback when the user has no Spend Credits or prefers on-chain pay-in (BTC, ETH, USDC on supported networks, etc.).

## MCP

1. `quote` — show crypto total for chosen `crypto_slug` if specified
2. User confirms
3. `create_order` with `payment_method=crypto` and optional `crypto_slug`
4. Return `payment_url` to the user — they complete payment in browser
5. Poll `get_order` until status advances past awaiting payment
6. `reveal_codes` after delivery

**User message:** "Open this link to pay — I'll watch for confirmation."

Do not narrate deposit addresses in group settings unless the user is alone with the agent.

## vs SCC

| | SCC | Crypto link |
| --- | --- | --- |
| Speed | Instant | Waits for chain confirmation |
| Extra step | None | User pays on the web |

Always prefer SCC when balance covers the order.
