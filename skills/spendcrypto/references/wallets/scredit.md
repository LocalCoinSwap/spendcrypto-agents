# Wallet: Spend Credits (SCC)

Prepaid USD balance on the user's SpendCrypto account. Fastest agent checkout — no chain wait.

## Requirements

- SpendCrypto account (OAuth or API key on MCP)
- Sufficient balance at [spendcrypto.com/my-credits](https://spendcrypto.com/my-credits)

## MCP

1. `quote` with default or explicit SCC line — show user the SCC total
2. User confirms
3. `create_order` with `payment_method=scc`
4. Order moves to fulfillment immediately — poll `get_order`, then `reveal_codes`

## REST

`POST /order-cart/` with `cryptoSlug: "SCC"`.

## When SCC is insufficient

Quote still returns crypto alternatives. Offer to fund credits or use `payment_method=crypto` for a payment link.
