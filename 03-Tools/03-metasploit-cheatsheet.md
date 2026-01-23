# Metasploit Cheat Sheet

## Overview
Metasploit Framework is a powerful exploitation and post-exploitation tool with thousands of modules.

## Basic Workflow
1. Search for a module
2. Select the module with `use`
3. Configure options (RHOSTS, LHOST, payload, etc.)
4. Run the exploit or auxiliary
5. Manage sessions and document results

## Common Commands
```bash
msfconsole                  # Launch Metasploit

search <keyword>            # Search modules
use exploit/...             # Load a module
show options                # View module options
set RHOSTS <target>         # Set target host(s)
set RPORT <port>            # Set target port
set LHOST <your IP>         # Local host for reverse payloads
set PAYLOAD <payload>       # Choose payload
run / exploit               # Execute module

sessions -l                 # List sessions
sessions -i 1               # Interact with session 1
jobs                        # Show background jobs
```

## Meterpreter Basics
```bash
sysinfo
getuid
ps
shell
download / upload <file>
hashdump
search -f *.config
```

## Quick Wins
- Start with recon before exploitation
- Match OS/architecture carefully to avoid crashes
- Use `sessions` for post-exploitation
- Save evidence for reports
