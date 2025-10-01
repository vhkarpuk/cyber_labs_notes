# Wireshark Cheat Sheet

## Overview
Wireshark is a network protocol analyzer used for packet capture and inspection.

## Basic Workflow
1. Start capture on desired interface
2. Apply filters to isolate relevant traffic
3. Inspect protocols, payloads, and streams
4. Export packets or follow sessions

## Common Filters
```text
ip.addr == 10.10.10.5      # Traffic to/from specific host
tcp.port == 80             # Filter by port
http                       # Only HTTP traffic
ftp or ftp-data            # FTP traffic
dns                        # DNS traffic
tcp.flags.syn == 1         # SYN packets
```

## Useful Features
- **Follow TCP/UDP Stream**: Rebuild conversations
- **Statistics → Protocol Hierarchy**: Traffic breakdown
- **Statistics → Conversations**: Host communication pairs
- **Export Objects (HTTP, SMB, etc.)**: Extract files

## Quick Wins
- Use filters early to reduce noise
- Look for credentials in cleartext protocols
- Correlate timestamps with attack windows
