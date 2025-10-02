# Finding: Unauthenticated Redis Service on TCP/6379

## Summary
Redis accessible without authentication; direct read access to keys/values.

## Evidence (sanitized)
- `6379/tcp open redis` via Nmap.
- `redis-cli -h <TARGET_IP>` → `INFO keyspace`, `SCAN`, `GET` (value redacted).

## Impact
Secrets/sessions/config exposure; potential lateral movement.

## Severity
High (context-dependent).

## Mappings
OWASP A05; CWE-306; CWE-200.

## Recommendations
Restrict bind/firewall, enable AUTH/ACL, use TLS, reduce admin commands, avoid long-lived secrets, monitor.

## Re-test
External access blocked or requires TLS/AUTH; unauthorized denied; no sensitive keys without TTLs.
