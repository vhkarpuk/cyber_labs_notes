# Preignition Write-up
**Prepared by:** 0ne-nine9  

---

## 📝 README
The target exposed an HTTP service running **nginx 1.14.2** on port 80.  
The default nginx page suggested a fresh/misconfigured installation with no navigation links.  
As such, **directory brute forcing (dir busting)** was required to uncover hidden resources.  

Using **Gobuster** with a custom wordlist, the path `/admin.php` was discovered and returned a **200 OK** status code.  
Navigating manually to this page revealed a login panel. Testing default credentials `admin:admin` successfully granted access and exposed the flag.  

**Objective completed.**