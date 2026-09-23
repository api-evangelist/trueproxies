---
name: buy-and-pay-invoice
description: Price an offer, create a TrueProxies invoice and pay it without double-charging.
api: TrueProxies Customer API
operations:
- get_v1_catalog_priced
- post_v1_invoices
- post_v1_invoices_id_pay
- get_v1_invoices_id
---
# Buy and pay

1. `get_v1_catalog_priced` — offers priced for the invoice payer (reseller terms when acting for an owned customer via `customer_id`).
2. `post_v1_invoices` with an `Idempotency-Key` (requires billing:write or reseller:purchase). Prices and discount are snapshotted; a floor conflict returns 409.
3. `post_v1_invoices_id_pay` with its own `Idempotency-Key`. Insufficient funds return 409 with `balance_cents` and `needed_cents`.
4. Never automatically retry an uncertain payment: first read `get_v1_invoices_id`. A replay with the same key returns `Idempotency-Replayed: true` rather than paying twice.

Amounts are integer cents. There is no refund operation in the API — refunds go through support under the Refund Policy.
