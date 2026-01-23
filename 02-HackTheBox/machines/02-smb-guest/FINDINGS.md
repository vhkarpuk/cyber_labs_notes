# Finding: SMB Guest/Anonymous Access

## Summary
Unauthenticated users can list/download files from SMB share(s).

## Evidence (sanitized)
- Nmap: 445/tcp open; service banner.
- `smbclient -L //<TARGET_IP> -N` shows shares; readable share accessed anonymously.

## Impact
Information disclosure; possible credential leakage; supports lateral movement.

## Severity
Medium–High (depends on content).

## Mappings
OWASP A05; CWE-284; CWE-200.

## Recommendations
Disable Guest/Anonymous; tighten share/NTFS ACLs; disable SMBv1; monitor access; remove sensitive files from shares.

## Re-test
Guest listing denied; authenticated access scoped; sensitive content not publicly readable.
