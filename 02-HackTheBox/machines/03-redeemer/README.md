# HTB Starting Point — Redeemer (Redis) | Professional Walkthrough

**Difficulty:** Very Easy  •  **Category:** Service Enumeration / Misconfiguration  •  **OS:** Linux  •  **Focus:** Redis (TCP/6379)

> Sanitized: no flags, credentials, or live target details.

## Executive Summary
The target exposes **Redis** on **TCP/6379** with **no authentication**. We confirm with `nmap`, safely enumerate with `redis-cli` (`INFO keyspace`, `SCAN`), and read a benign value. In real environments this often exposes sessions, secrets, and config.

**Risks:** OWASP A05; CWE-306; CWE-200.

## Phases (condensed)
**Recon (ports):**
```bash
sudo nmap -Pn -sS --min-rate 3000 -p- <TARGET_IP> -oA nmap/full
```
**Service/Version:**
```bash
sudo nmap -Pn -sS -sV -sC -p 6379 <TARGET_IP> -oA nmap/sv
```
**Redis interaction:**
```bash
redis-cli -h <TARGET_IP> -p 6379
> INFO keyspace
> SCAN 0 MATCH *flag* COUNT 100
> TYPE flag
> GET flag      # redacted
```

## Remediation (summary)
Bind to loopback/VPC, enable AUTH/ACL (Redis ≥6), use TLS, reduce command surface, avoid long-lived secrets, monitor usage.

See `FINDINGS.md` for detailed risk & re-test steps.
