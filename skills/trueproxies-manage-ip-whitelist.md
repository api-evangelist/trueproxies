---
name: manage-ip-whitelist
description: Add, list and remove IP whitelist entries on a TrueProxies service.
api: TrueProxies Customer API
operations:
- get_v1_services_id_whitelist
- post_v1_services_id_whitelist
- delete_v1_services_id_whitelist_entryId
---
# Manage the IP whitelist

1. `get_v1_services_id_whitelist` — addresses allowed to connect without a proxy password.
2. `post_v1_services_id_whitelist` — a public address or supported CIDR, up to 50 entries per service. An address assigned to another service returns CONFLICT. This write has no idempotency key: after an uncertain response, list entries before retrying.
3. `delete_v1_services_id_whitelist_entryId` — returns 204; a subsequent read confirms removal. This is the reversal for step 2.
