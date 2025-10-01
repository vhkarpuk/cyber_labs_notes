# Splunk Cheat Sheet

## Overview
Splunk is a SIEM platform for log management, searching, and analysis. It helps identify patterns, anomalies, and security events.

## Basic Workflow
1. Ingest log sources (system, network, application)
2. Use SPL (Search Processing Language) for queries
3. Build dashboards and alerts for monitoring
4. Correlate events with threat intelligence

## Common SPL Queries
```spl
index=main error                     # Find error messages
index=web status=404                 # HTTP 404 errors
index=firewall action=blocked        # Blocked firewall traffic
index=syslog user="admin"            # Admin logins
index=* | stats count by sourcetype  # Events grouped by source type
```

## Useful Features
- Dashboards for real-time monitoring
- Alerts for suspicious activity
- Lookups to enrich logs with external data
- Correlation searches

## Quick Wins
- Build saved searches for frequent queries
- Use alerts to notify of anomalies
- Combine with threat intel feeds for context
