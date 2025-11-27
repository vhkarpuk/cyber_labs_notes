# Sequel Write-up
**Prepared by:** 0ne-nine9

---

## 📝 README
The target exposed a **MariaDB 10.3.27** service running on port `3306/tcp`.  
MariaDB is a relational SQL database used to structure data in tables, rows, and fields.

This instance allowed **anonymous root access** without requiring a password.  
Using the MariaDB client, it was possible to enumerate databases, select the `htb` database, and read the contents of the `config` table.

Inside this table, the flag was stored in the corresponding `value` field.

**Objective completed successfully.**
