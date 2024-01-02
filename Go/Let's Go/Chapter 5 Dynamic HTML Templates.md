# 5.1 Displaying Dynamic Data

- `{{ }}` - used in Go's `html/template` package to signify placeholder information for dynamic data within your templates.
- `<pre>` an HTML tag used to define pre-formatted text.
- `<code>` an HTML tag used to define a piece of computer code.
- `<time>` an HTML tag used to enclose a date/time. Also can be used to format the date/time into a machine readable way.

## Rendering multiple pieces of data

- Go’s `html/template` allows you to pass in _only one_ item of dynamic data.
- To render multiple pieces we must wrap our dynamic data in a struct which acts like a **single** _‘holding structure’_ for your data.

### Dynamic Content Escaping

- The `html/template` package in Go automatically _protects_ your data from being misused. It's like writing a note about your Lego creation and giving it to a friend.

- For example, if you wrote a note saying, "My spaceship has a
  `<script>alert('Lego theft')</script>` engine", the `html/template` package changes this to something safe like so:
  ``&lt;script&gt;alert(&#39;Lego theft&#39;)&lt;/script&gt;`

- The `html/template` package also knows where your note will be used. If it's on a website, it knows not to let people run scripts. If it's in a book, it knows not to let people click on links.

## Nested Templates

- When invoking one template from another, dot must be passed or pipelined to the template being invoked. This can be done at the end of the template like below.
- _Example:_

```go
{{template "main" .}} {{block "sidebar" .}}{{end}}
```

## HTML comments

- Go's `html/template` always strips your template of any comments.
- Avoids XSS attacks when rendering dynamic content.

# 5.2 Template actions and functions

## Controlling dynamic data with...

- `{{if}}`,`{{with}}`, &`{{range}}`
  ![[Pasted image 20231116102303.png]]
  Notes on the above
- The `{{else}}` is optional
- Empty values(0, nil , interface val, string of length 0) are `false`

- `{{with}}` in Go's template package is used to temporarily set the context of a variable within a block. This allows for cleaner and more concise code when accessing nested data.
*Example*
```go
{{define "main"}}
	{{with .Snippet}}
		<strong>{{.Title}}</strong>
	{{end}}
{{end}}
```

- In this example, `{{with .Snippet}}` sets the context to the `Snippet` field, allowing `.Title` to be equivalent to `Snippet.Title` within the block. This reduces the need to explicitly write `Snippet` before `Title` each time it's accessed.

## Combining functions 
- You can combine functions with go's template library like so 
*Example*
```go 
{{if (gt (len .Foo) 99)}} C1 {{end}}
```
- This will will render C1 if the length of .Foo is > 99
## Controlling loop behavior 
- You can use functions such as `{{break}}` and `{{continue}}` within range loops. 
*Example*
```go 
{{range .Foo}}  
// Skip this iteration if the .ID value equals 99. 
	{{if eq .ID 99}}
		{{continue}} 
	{{end}}
	// End the loop if the .ID value equals 199
	{{if eq .ID 199}}
		{{break}} 
	{{end}}
{{end}}
```

# 5.3 Caching templates
- A Go map type looks like this:
```go
map[KeyType]ValueType
```
- We're going to place the parsed templates within the map so it's quick to retrieve rather than parsing them every single time. 
*Example*
```go
map[string]*template.Template
```
- The string is the key and the value is a pointer to template.Template, a struct used to hold the parsed values of the template. 

- `file.Glob()`:  used to match a pattern and return the names of all files that match the pattern. If there are no matching files, it returns `nil`
- `.Base()` returns the last element within a file path. 
*Example*
```go
path := "/home/user/example.txt"
file := filepath.Base(path) 
fmt.Println(file)
// prints "example.txt"
```

## Templates and parsing 
- `template.parseFiles()`: Reads the content of files, parses them into a * template.Template, and returns it. This function is used to prepare templates for execution.
- **\*template.Template**: A data structure that holds the contents of a parsed template. 
	- Holds information of the template such as: placeholders(variables),
	- Structure of the template(indentations, blocks, conditionals, loops), and actions to be performed when executing the template (such as replacing placeholders with actual values)

- `.Execute()`: Apply a parsed template to data and generate an output. 
	- Takes *2 arguments:* an \**io.Writer* where the output will be written and the *data* to be applied to the template. 
		-  In Go, an `io.Writer` is an interface that represents a destination to which you can write data.  It's a common interface in Go's standard library for which data needs to be written to. 
	- A variable can hold a slice of \*template.Template objects, but the order of them is significant especially when .Execute() is called. It will execute in the order of it. 
*Example*
- File named "*message.txt*"
```go 
{{.Name}} is a {{.Occupation}}
```

*Main file*
```go
type User struct {
Name string
Occupation string 
} 

func main() {
	user := User{"John Doe", "gardener"}
	tmp, err := template.ParseFiles("message.txt") 
	if err != nil { 
		log.Fatal(err) 
	}
	err2 := tmp.Execute(os.Stdout, user) 
	if err2 != nil { 
	log.Fatal(err2) 
	}
}
```
- *In this example we're creating an instance of a User, custom struct, with a name and occupation. We're then parsing the message file to get the information of the template as a \*template.Template stored in the variable tmp. We then execute the template with the user data to fill the templates placeholders and the result is:
   "John Doe is a gardener"*

## Variadic functions (...)
- A **Variadic function** is one in which can accept an arbitrary amount of arguments.
-  In Go, you can define a variadic function by using the `...` operator followed by the type of the arguments
*Example*
```go 
func sum(nums ...int){ 
	total := 0 
	for _, num := range nums { 
	    total += num 
	} 
	fmt.Println(total)
} 

func main() { 
	sum(1, 2) // 3
	sum(1, 2, 3) // 6
	sum(1, 2, 3, 4) // 10 
}
```
- *Note: If you have a slice that you'd like to pass to a variadic function, then you would include `...` after the input. This expands the slice into individual arguments that get passed to the function.*

*Example*
```go 
nums := []int{1, 2, 3} 
sum(nums...)
```

# 5.4 Catching runtime errors 
- We can use a buffer when rendering a template and check for errors, render the error if there is one, and render the template to the http.ResponseWriter. 
- If we don't use a buffer then the user can receive an error while getting a 200 OK status and or receive incomplete content. 
# 5.5 Common Dynamic Data
- There can be common dynamic data we sometimes would like to include within pages such as profile pictures, user names, or even the date. We can include them within templates to carry over and simplify things.
# 5.6 Custom template functions
- **template.FuncMap:** A type of map that associates string key values with *function* values. 
	- Often used with the html/template & text/template packages that c*an be used to create custom functions* that can be used within HTML/Text templates.

