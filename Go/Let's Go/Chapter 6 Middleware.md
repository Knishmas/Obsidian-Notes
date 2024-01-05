- **Middleware:** Software that acts as a bridge allowing different parts of an application to communicate and manage date.
	- *Analogy:* Think about a postman(middleware) who sends and receives mail between houses in a neighborhood(different parts of an application). 
	- Middleware could be anything from database access, user authentication, data validation, error handling, etc.
	- Allows the automation of repetitive tasks. 
## 6.1 How middleware works
- *"You can think of a Go web application as a chain of `ServeHTTP()` methods being called one after another"*
- Our go application listens to requests and they trigger servemux's `ServeHTTP()` method. This finds the request and triggers it's handler's `ServeHTTP()` function.  *A chain of `ServeHTTP()` methods.*
- With middleware we can insert it into the chain before our `ServeHTTP()` methods. This way it perform it's function such as logging requests before serving the request
- **Template for creating your own middleware** 
```go 
func myMiddleware(next http.Handler) http.Handler {  
	fn := func(w http.ResponseWriter, r *http.Request) {
		// TODO: Execute our middleware logic here...
		next.ServeHTTP(w, r) 
	}
		return http.HandlerFunc(fn) 
}
```
- This middleware function creates a function that applies the middleware before serving the next HTTP handler, *effectively returning a handler that combines the middleware functionality and the next chained HTTP handler*.

- **Simplified middleware template**
```go 
func myMiddleware(next http.Handler) http.Handler {  
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
	// TODO: Execute our middleware logic here...
	next.ServeHTTP(w, r) 
	})
}
```
- Anonymizes the function
- Shorter and most common pattern. 
- **Positioning middleware**
	- *The position of your middleware is important and will effect the behavior of your application.*
	- **myMiddleware → servemux → application handler**
		- If it's placed before the servemux handler in the chain, then the middleware will act on all requests, this is useful and common for logging all requests. 
	- **servemux → myMiddleware → application handler**
		- In cases where you don't want your middleware acting on every handler, such as authentication (only acting on specific handlers), then you would wrap the specific app handler(s). 

## 6.2 Setting Security Headers 

 - **Content-Security-Policy (CSP)**: This header restricts where your webpage loads its resources from, helping prevent various attacks.
- **Referrer-Policy**: Controls what information is included in the Referer header when a user leaves your webpage.
- **X-Content-Type-Options: nosniff**: Instructs browsers not to guess the content-type of the response, preventing content-sniffing attacks.
-  **X-Frame-Options: deny**: Helps prevent clickjacking attacks in older browsers that don't support CSP headers.
-  **X-XSS-Protection: 0**: Disables the blocking of cross-site scripting attacks, especially useful when using CSP headers.

- These security headers should be on every request we receive, so we must execute the middleware before our servemux.
	- *secureHeaders → servemux → application handler.*
	- To accomplish this, we'll wrap our servemux with the `setHeaders` func. 
	- 