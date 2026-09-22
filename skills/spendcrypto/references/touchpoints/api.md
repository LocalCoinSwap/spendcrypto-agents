# Touchpoint: Partner REST API

> Internal only — for scripts and B2B integrators without MCP.

**Base:** `https://api.spendcrypto.com/api/v1/`  
**OpenAPI:** [spendcrypto.com/developers/openapi.json](https://spendcrypto.com/developers/openapi.json)  
**Explorer:** [spendcrypto.com/developers/api](https://spendcrypto.com/developers/api)

## Auth

```
Authorization: Api-Key YOUR_KEY
X-Api-Key: YOUR_KEY
X-Client: agent
```

Optional: `Idempotency-Key` on `POST /order-cart/` (recommended for agents).

## Prepaid SCC flow

1. Fund Spend Credits — `/my-credits` on web
2. `POST /order-cart/` with `cryptoSlug: "SCC"`
3. `GET /order-cart/{sid}/` until delivered
4. `POST /order-cart/{sid}/reveal-codes/`

## Crypto payment link

Same as MCP `payment_method=crypto` — cart stays `AWAITING_USER_PAYMENT` until the user pays at `https://spendcrypto.com/order/{sid}`.

## Guest checkout

REST supports guest email + Turnstile on web; **MCP requires** a signed-in account (OAuth or API key).

MCP is the preferred agent surface; use REST when the host cannot run MCP.
