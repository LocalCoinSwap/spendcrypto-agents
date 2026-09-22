# Spending safeguards

> Internal only — never voice MCP, OAuth, API keys, or tool names to the user.

Real-money digital goods. Voucher codes and eSIM install data are **bearer assets** — like cash.

## Universal rules

- **Confirm before buy.** Product, denomination, exact price, payment method. Wait for explicit approval every time.
- **Never auto-approve** `create_order`, `cancel_order`, or `reveal_codes`.
- **Codes are secret.** Do not paste voucher PINs or eSIM LPA strings into group chats, shared threads, or TTS.
- **Two-step delivery.** Order GET redacts codes; call `reveal_codes` only when the user is ready to receive them privately.
- **Dedicated agent account.** Use a SpendCrypto account funded for agent spend — not a personal wallet with large balances.
- **Daily cap.** ~$5k USD equivalent per account per day (platform limit).
- **Log purchases.** Order sid, product, amount, payment method, timestamp — never log raw codes.

Terms: [spendcrypto.com/terms](https://spendcrypto.com/terms)

## Cursor / Claude Code

Keep read tools in `autoApprove`; **exclude** write tools:

```json
{
  "mcpServers": {
    "spendcrypto": {
      "url": "https://api.spendcrypto.com/mcp",
      "headers": { "Authorization": "Api-Key YOUR_KEY" },
      "autoApprove": [
        "search_products", "get_product", "quote",
        "get_order", "list_orders", "get_account", "get_esim_usage"
      ]
    }
  }
}
```

## OAuth sessions

Claude and Grok use OAuth — user signs in with email OTP and approves scopes once. Treat the session as that user's Spend Credits balance; do not share connectors across unrelated users.
