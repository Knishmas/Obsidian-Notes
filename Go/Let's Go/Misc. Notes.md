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
## Pointers and references (& and * ) 
- **"&"** used to get the memory address of a variable, the reference operator. 
*Example:* 
```go
	var x int = 1 
	fmt.Println(&x) // prints the memory address of x 
```
- **" * "** used to access the value stored at a specific memory address, known as dereferencing.
*Example:* 
```go
	var x int = 1 
	var p *int = &x
	fmt.Println(*p*) // prints the value of x 
```

## Receivers and methods 
- **Receiver:** a special type of parameter within a function that defines the type on which the method can be called on. 
 *Example:* 
 ```go
 func (logger *Logger) Log(message string) {
    fmt.Println(message)
}
```
- In this example `(logger *Logger)` is our receiver, the Log method may only be called on a Logger type. 
- `Log` is our Function name and `message string` is our regular parameter, it defines the input of the method. 
- To call the Logger method, you need to have an instance of Logger (or a pointer to one), and you call it like so: 
```go 
logger := &Logger{}
logger.Log("Hello, world!")
```

## Templates 
- A tool used for generating text output 
- Consists of regular text with actions, special instructions enclosed within `{{}}` 
- ``{{define}}`` defines a new template that can be invoked later. 
	- *Example* `{{define "name"}} T1 {{end}}` 
	- `"name"` is the name of the template, `T1` is the content of the template
- The defined template can then be invoked using the `{{template}}`
	- *Example* 	
```go
{{define "T1" -}}
Hello {{ . }}!
{{- end -}}

{{ template "T1" "World" }}
{{ template "T1" }}
{{ template "T1" "everybody" }}
```
The output will be: 
```html
Hello World!
Hello <no value>!
Hello everybody!
```

- ``{{block}}`` Defines a section of a template that can be overriden by other templates. 
	- *Example *
```go
{{define "base"}}
Hello, {{block "name" .}}{{.}}{{end}}!
{{end}}
{{template "base" "World"}}

```
- If no  template is provided, the default content of the block (denoted by `{{.}}`) is used.
```go
{{define "name"}}Universe{{end}}`
``` 
- *will generate: `Hello Universe`*
## Dot (.) in Go's text/template package
 - The dot (`.`) in Go's `text/template` package is a special identifier that represents the current item or data in the context, which can be a variable, a map, a slice, or any other data type.
- It is used in various parts of the template, such as within actions (`{{with .}}`, `{{range .}}`), or in pipelines (`{{. | printf "%s"}}`). Its value can change depending on the context. For example, in a `range` action, the dot would represent each element of the iterable being processed. Excellent for referencing and manipulating the current context or data within a template.
 - *Example*
```go
go package main

import ( "os" "text/template" )

func main() { 
t := template.Must(template.New("test").Parse("Hello, {{.}}")) 
t.Execute(os.Stdout, []string{"World", "Gophers"}) }
```
**Output:** "Hello, World Hello, Gophers"

##  http.Handler(s)
- An interface capable of handling http requests. 
- Defined by the `ServeHTTP(ResponseWriter, *Request)` method. 
	- Any type that utilizes this method can be considered a http.handler.
- `ServeHTTP()` is part of the of the `http.Handler` interface, is utilized for processing requests, and generating responses. 

*Example*
```go
type MyHandler struct{}

func (h MyHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
   fmt.Fprint(w, "Hello, World!")
}
```
- When a requests comes in `"Hello World"` is printed. 

- **Handler Parameters:** `(w http.ResponseWriter, r *http.Request)`
	- `ResponseWriter:` An interface that allows the handler to construct a HTTP response. Contains methods for setting headers, status code, and writing the response body. 
	- `*Request`: a pointer to a `Request` object, which contains all the information about the incoming HTTP request, including the method, URL, headers, and body. 

