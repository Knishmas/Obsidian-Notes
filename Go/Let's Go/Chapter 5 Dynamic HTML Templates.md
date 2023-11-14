# 5.1 Displaying Dynamic Data 
- `{{ }}` - used in Go's `html/template` package to signify placeholder information for dynamic data within your templates. 
- `<pre>` an HTML tag used to define pre-formatted text. 
- `<code>` an HTML tag used to define a piece of computer code. 
- `<time>` an HTML tag used to enclose a date/time. Also can be used to format the date/time into a machine readable way. 
## Rendering multiple pieces of data 
- Go’s `html/template` allows you to pass in *only one* item of dynamic data. 
- To render multiple pieces we must  wrap our dynamic data in a struct which acts like a **single** *‘holding structure’* for your data.
### Dynamic Content Escaping

- The `html/template` package in Go automatically *protects* your data from being misused.  It's like writing a note about your Lego creation and giving it to a friend.

- For example, if you wrote a note saying, "My spaceship has a 
```<script>alert('Lego theft')</script>``` engine", the `html/template` package changes this to something safe like so: 
```&lt;script&gt;alert(&#39;Lego theft&#39;)&lt;/script&gt;``

- The `html/template` package also knows where your note will be used. If it's on a website, it knows not to let people run scripts. If it's in a book, it knows not to let people click on links.

## Nested Templates 
- When invoking one template from another, dot must be passed or pipelined to the template being invoked.  This can be done at the end of the template like below. 
- *Example:*
```go 
{{template "main" .}} {{block "sidebar" .}}{{end}}
```

## HTML comments 
- Go's `html/template` always strips your template of any comments.  
- Avoids XSS attacks when rendering dynamic content.