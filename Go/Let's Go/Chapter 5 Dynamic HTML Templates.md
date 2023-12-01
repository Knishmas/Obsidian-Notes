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

- `file.Glob()`: Returns the last element of a given file path. 
*Example*
```go
path := "/home/user/example.txt"
file := filepath.Base(path) 
fmt.Println(file)
// prints "example.txt"
```
