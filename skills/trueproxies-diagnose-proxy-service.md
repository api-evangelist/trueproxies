---
name: diagnose-proxy-service
description: Tell a TrueProxies service problem apart from a target that is refusing you.
api: TrueProxies Customer API
operations:
- get_v1_services_id
- post_v1_services_id_check
- get_v1_services_id_live_metrics
- get_v1_services_id_analytics
- get_v1_services_id_usage
---
# Diagnose a proxy service

1. `get_v1_services_id` — status, expiry, capabilities and effective limits.
2. `post_v1_services_id_check` — runs one request through the service from TrueProxies' side (rate limited to a few checks a minute).
3. `get_v1_services_id_live_metrics` — ten-second traffic rates; read `last_activity_at` for freshness.
4. `get_v1_services_id_analytics` (24h, 7d or 30d; can lag) and `get_v1_services_id_usage` (bytes; decimal GB balances) for longer-range evidence.
