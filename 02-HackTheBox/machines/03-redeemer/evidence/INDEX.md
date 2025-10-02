# Evidence Index (Template)

Suggested layout:
```
00-context/   # date, uname, tool versions
01-vpn/       # tun interface + routes (if applicable)
02-scan/      # raw nmap outputs (.nmap/.xml)
03-service/   # CLI transcripts (redacted as needed)
04-screens/   # 1–2 PNGs; blur/box secrets
```
Minimal commands:
```bash
date -u > evidence/00-context/timestamp_utc.txt
uname -a > evidence/00-context/uname.txt
nmap --version > evidence/00-context/nmap_version.txt

# Nmap scans
sudo nmap -Pn -sS --min-rate 3000 -p- <TARGET_IP> -oA evidence/02-scan/nmap_full
sudo nmap -Pn -sS -sV -sC -p <OPEN_PORTS> <TARGET_IP> -oA evidence/02-scan/nmap_sv
```
Replace secrets/flags with `<REDACTED>`; avoid publishing live IPs.
