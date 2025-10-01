# John the Ripper Cheat Sheet

## Overview
John the Ripper (JtR) is a password cracker for auditing password strength. It supports many hash formats and multiple attack modes.

## Basic Workflow
1. Extract or obtain password hashes
2. Convert with *2john utilities if needed (zip2john, rar2john, etc.)
3. Run John with wordlist, rules, mask, or incremental
4. Show cracked results

## Common Commands
```bash
# Crack with dictionary
john hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

# Show cracked results
john --show hashes.txt

# Specify format (example: NTLM)
john ntlm_hashes.txt --format=NT

# Mask attack (6-digit PIN)
john hashes.txt --mask=?d?d?d?d?d?d
```

## Useful Flags
- `--wordlist` : Use custom dictionary
- `--rules` : Apply mangling rules
- `--mask` : Define pattern
- `--incremental` : Brute-force mode
- `--session` : Save session

## Quick Wins
- Always identify hash type (`--format`)  
- Start with wordlist + rules before brute force  
- Document cracked passwords responsibly  
