# Mongod Write-up
**Prepared by:** dotguy  

---

## 📝 README
The target exposed a **MongoDB 3.6.8** instance on port `27017/tcp` alongside SSH on port `22/tcp`.  
MongoDB is a **NoSQL document-oriented database**, which organizes data in a hierarchy of **databases → collections → documents**.  

This particular MongoDB instance allowed **anonymous access** (no authentication), which enabled direct enumeration of databases and collections.  
By connecting with `mongosh`, the sensitive database `sensitive_information` was accessed.  
Inside it, the `flag` collection contained a document with the required flag value.  

**Objective completed.**