## **Command line flag** 
- In go a command line flag is a way to pass options to a program that are defined before the program's execution. 
*How is this useful?* 
- Flexibility and control. Used to modify the behavior of the program without having to change the program's source code or config files.
*Example* 
```go 
dsn := flag.String("dsn", "web:pass@/snippetbox?parseTime=true", "MySQL data source name")
```
- The ```dsn``` flag is used  to pass the MYSQL DSN string. If the flag isn't provided, then default value ```web:pass@/snippetbox?parseTime=true``` will be used. 
- Useful in situations where the MySQL DSN might change based on the environment, or if the user wants to connect to a different database. 
- The `flag` package in Go provides functionalities to define & manage these flags 