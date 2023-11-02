# 3.3 Dependency Injection 
*How can we make dependencies available?*
- **Best Practice:** Inject dependencies. 
	- Makes code more explicit, less error prone, and easier to unit test rather than using global variables. 
	- For applications with handlers all in the same file, a convenient way to inject dependencies is through creation of custom application structs.


# Side notes
- If you are creating a struct method and you want to alter an object, you need to make sure the method has a pointer receiver to the object in order to make an actual change to the object. Other wise if you just pass the object, go will change a copy of the object that is local to that method. 

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
```db, err := sql.Open("mysql", "web:pass@/snippetbox?parseTime=true")```
- 1st parameter - Driver name. *Find name through the DB's docs*
- 2nd parameter -  Data source name (DSN) or connection string. Describes how to connect to your DB.
	- Format of DSN will depend on your driver. *Refer to docs*
```parseTime=true```
- Driver specific - converts sql time/date to go time.time. obj. 
- 