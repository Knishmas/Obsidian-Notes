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

## Structs and interfaces in Go 
- **Interface:** A set of method signatures that a type must implement. Defines a contract for what a type should do, without saying anything about how to do it. 
	- They're a way to achieve polymorphism within Go, allowing different types to be used interchangeably if they implement the same interface. Makes code flexible and reusable 
	- Similar to a an object in Java 
- **Struct:** A custom data type that groups together fields of different types under a single name. 
	- Makes it easier to organize and manipulate related data.
	-  Similar to a class in Java 

## Value vs Pointer receivers 
- In Go methods can either have a value or pointer receiver. 
- **Value receiver:** The method will operate on a *copy* of the object. Any changes to the object are local to the method and doesn't affect the original object. 
- **Pointer receiver:** The method will operate directly on the original object. Any changes to the object will change the original. 
- Practical example: Fetching a user's information and being allowed to change it. We would use a method with a pointer receiver because we want to change the object holding the user's data. 