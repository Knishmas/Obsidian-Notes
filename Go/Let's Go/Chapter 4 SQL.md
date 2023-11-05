
# 4.1 Setting Up SQL 
 ```sql 
CREATE DATABASE snippetbox CHARACTER SET utf8mb4 
COLLATE utf8mb4_unicode_ci
 ```
 - **COLLATE:** Defines string comparison and how data is sorted within the database. 
 - **utf8mb4:** UTF-8 standard character encoding that includes almost all characters from all writing systems .
 - **Unicode:** Unicode standard
 - **ci:** Stands for 'case insensitive'. It will treat lower and upper cases as the same within the database. 

# 4.3 Modules & reproducible builds 
- **go.sum:** This file contains cryptographic checksums representing the content of the required packages. Similiar to package.json in node.js 
	**Serves two useful functions** 
	1. ```go mod verify``` verifies the checksum of the packages on your machine to make sure they're right. 
	2. ```go mod download``` downloads all the dependencies within the project. 

# 4.4 Creating a database connection pool

## Connecting web app to database
```sql.Open()```
- Function that initializes a new sql.DB object and returns a pool of DB connections. 
- Doesn't create any connections, just initializes pool for future use. 
- ```db.Ping()``` method that checks if the db is reachable, makes a connection. 
```db, err := sql.Open("mysql", "web:pass@/snippetbox?parseTime=true")```
- 1st parameter - Driver name. *Find name through the DB's docs*
- 2nd parameter -  Data source name (DSN) or connection string. Describes how to connect to your DB.
	- Format of DSN will depend on your driver. *Refer to docs*
```parseTime=true```
- Driver specific - converts sql time/date to go time.time. obj. 
- 