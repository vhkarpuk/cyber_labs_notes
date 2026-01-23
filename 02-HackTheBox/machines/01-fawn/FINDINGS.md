# Finding: Anonymous FTP Access on TCP/21

## Summary
Anonymous FTP allowed unauthenticated listing/download of files.

## Evidence (sanitized)
- Nmap shows 21/tcp open; `ftp-anon` indicates anonymous allowed.
- `ftp <TARGET_IP>` → `anonymous` login; `ls`, `get <file>`.

## Impact
Information disclosure; potential malicious uploads if write enabled; cleartext risk if not FTPS/SFTP.

## Severity
Medium–High (context-dependent).

## Mappings
OWASP A05; CWE-319; CWE-200.

## Recommendations
Disable anonymous, enforce auth, migrate to SFTP/FTPS, restrict directories, monitor.

## Re-test
Anonymous denied; authenticated users restricted; encrypted transfer as policy dictates.
