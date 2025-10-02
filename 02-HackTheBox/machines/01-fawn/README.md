# HTB Starting Point — Fawn (FTP) | Professional Walkthrough

**Difficulty:** Very Easy  •  **Category:** Service Enumeration / Misconfiguration  •  **Focus:** FTP (TCP/21, Anonymous)

> Sanitized: no flags or live target details.

## Executive Summary
**FTP (TCP/21)** allows **anonymous** login, enabling unauthenticated listing/download of files. Demonstrates Security Misconfiguration and, if cleartext only, CWE-319.

## Phases (condensed)
**Recon (ports):**
```bash
sudo nmap -Pn -sS --min-rate 3000 -p- <TARGET_IP> -oA nmap/full
```
**Service/Version & scripts:**
```bash
sudo nmap -Pn -sS -sV -sC -p21 <TARGET_IP> -oA nmap/sv
# Expect ftp-anon: Anonymous FTP login allowed
```
**FTP interaction:**
```bash
ftp <TARGET_IP>
# user: anonymous ; pass: <blank>
ftp> ls
ftp> get <file>   # saved to current local dir
```

## Remediation (summary)
Disable anonymous or isolate to non-sensitive read-only area; require auth; prefer SFTP/FTPS; review permissions; monitor.

See `FINDINGS.md` for risk & re-test.
