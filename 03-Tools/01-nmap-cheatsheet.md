# Nmap Cheat Sheet

## Overview
Nmap is a network scanner used to discover hosts and services. It supports port scanning, service enumeration, OS detection, and scripting for vulnerability discovery.

## Basic Workflow
1. Identify live hosts
2. Scan ports (common or full range)
3. Detect service versions
4. Save results for reporting

## Common Commands
```bash
# Default scan (1000 common ports)
nmap <target>

# Service/version detection + default scripts
nmap -sV -sC -oN scan.txt <target>

# Full TCP port scan
nmap -p- <target>

# Aggressive scan (OS, version, scripts, traceroute)
nmap -A <target>

# Quick UDP top 200 ports
nmap -sU --top-ports 200 <target>
```

## Useful Flags
- `-Pn` : Skip host discovery (treat hosts as online)
- `-p 80,443,8080` : Scan specific ports
- `--min-rate 5000` : Speed up scan rate
- `-oN/-oG/-oX` : Save output in normal, greppable, or XML format

## Quick Wins
- Start with `-sC -sV` for baseline enumeration
- Always run `-p-` if common scans show little
- Follow up high-value services (SMB, HTTP, SSH) with dedicated tools
