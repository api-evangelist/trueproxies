---
name: rotate-proxy-password
description: Rotate a TrueProxies service's proxy password safely, with an idempotent retry and the two-minute overlap in mind.
api: TrueProxies Customer API
operations:
- get_v1_services
- post_v1_services_id_rotate_password
- get_v1_services_id_secret
---
# Rotate a proxy password

1. `get_v1_services` — find the service id (current services by default; cursor pagination with `cursor`/`limit`).
2. `post_v1_services_id_rotate_password` — send an `Idempotency-Key` formatted as Unix-milliseconds creation time, a dot and a UUID. The response carries the new password; the previous one stays valid for a two-minute overlap, so update every client promptly.
3. On an uncertain response, retry with the SAME key within 23 hours — a replay does not rotate again. Without a key, call `get_v1_services_id_secret` (proxy:read) before deciding whether another rotation is needed.

Scopes: proxy:write to rotate, proxy:read to read the secret. Treat all returned credentials as secrets. On 429, wait for `Retry-After`.
