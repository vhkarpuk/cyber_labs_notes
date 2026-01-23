# HTB: Fawn (FTP) — Evidence (Sanitized, text-only)

Timestamp (UTC): <YYYY-MM-DD HH:MM:SS UTC>
Environment: Linux <host> <kernel_version> #1 SMP <date> <arch>
Tool versions:
- Nmap 7.94SVN
- ftp GNU Inetutils

# VPN / Reachability 
sudo openvpn <vpn_name>_ovpn

ping <target_ip>


# Scans (commands + sanitized outputs)
sudo nmap -p- -sV <TARGET_IP> 
Host: <TARGET_IP> (target)  Status: Up
PORT      STATE SERVICE
21/tcp    open  ftp

# FTP anonymous session (sanitized transcript)
ftp <TARGET_IP>
Connected to <TARGET_IP>.
220 (vsFTPd 3.0.3)
Name (<TARGET_IP>:<local_user>): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 0        0             123 Jan 01 00:00  <benign_file>.txt
226 Directory send OK.
ftp> get <benign_file>.txt
local: <benign_file>.txt remote: <benign_file>.txt
150 Opening BINARY mode data connection for <benign_file>.txt (123 bytes).
226 Transfer complete.
123 bytes received in 0.00 secs (1.2 MB/s)
ftp> bye
221 Goodbye.

# Retrieved file content (redacted)
<REDACTED>

# Notes
- Replace placeholders `<TARGET_IP>`, `<local_user>`, `<benign_file>` with your values if desired.
- Do not include flags/credentials; keep sensitive values as `<REDACTED>`.
