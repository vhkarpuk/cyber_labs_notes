# HTB — SMB Guest Access | Professional Walkthrough

**Difficulty:** Easy  •  **Category:** Access Control / Enumeration  •  **Focus:** SMB (TCP/445), Guest/Anonymous

> Sanitized: no flags or live details.

## Executive Summary
SMB permits **Guest/Anonymous** access to at least one share, enabling unauthenticated listing/download. Classic access control issue.

## Phases (condensed)
**Recon (ports):**
```bash
sudo nmap -Pn -sS --min-rate 3000 -p- <TARGET_IP> -oA nmap/full
```
**SMB enumeration:**
```bash
sudo nmap -Pn -sS -sV -sC -p445,139 <TARGET_IP> -oA nmap/sv
smbclient -L //<TARGET_IP> -N
smbmap -H <TARGET_IP> -u "" -p ""
```
**Access readable share:**
```bash
smbclient //<TARGET_IP>/<Share> -N
smb: \> ls
smb: \> get <file>
```

## Remediation (summary)
Disable Guest/Anonymous; least-privilege ACLs; disable SMBv1; consider signing/encryption; remove sensitive files from shares.

See `FINDINGS.md` for full details.
