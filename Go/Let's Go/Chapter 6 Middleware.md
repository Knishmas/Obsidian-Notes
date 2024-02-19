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
*Note:  Functions are not considered types they are function types and therefore can't implement an interface. An `http.Handler` is expected to be a type that has a `ServeHTTP` method, not a function itself. But if we wrap the func with `http.Handler `  it satisfies the `http.Handler` interface.*
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

- **Flow of Control** 
	-  *secureHeaders → servemux → application handler → servemux → secureHeaders*
	- The flow of control describes the sequence of execution in our Go program.
	- Similar to DFS (refer to: [[Pre and post DFS]] ), code before `next.ServeHTTP()` executes down the chain, and code after it executes when returning up the chain.
	- We progressively move down the chain with `next.ServeHTTP()` calls until reaching the final handler that produces an actual HTTP response. We then work our way back up the chain. 

 - **Early returns** 
	- Similar to Depth-First Search (DFS), you can prematurely exit the `ServeHTTP()` chain and return upwards.
	-  This can be beneficial, for instance, when a user is unauthorized. In such cases, you might want to redirect them to a `403 Forbidden` status and halt further execution down the chain.
*Example*
```go 
func myMiddleware(next http.Handler) http.Handler {  
	return http.HandlerFunc(func(w http.ResponseWriter,        r *http.Request) {
	
		// If the user isn't authorized send a 403 
		// Forbidden status and return to stop
		// executing the chain.  
	if !isAuthorized(r) {
		w.WriteHeader(http.StatusForbidden)
		return
}
	// Otherwise, call the next handler in the chain.
	next.ServeHTTP(w, r)
})
}
```

- **Debugging CSP issues**
	- Use developer tools for debugging Content Security Policy (CSP) issues.
	- Regularly check logs for unexpected problems.
	- Blocked resources in Firefox are shown as errors in the console logs.

## 6.3 Request Logging 
- 
## 6.4 Panic Recovery 
*What's a panic?*
	- **Panic**: In Go, a panic is an unexpected error that leads to immediate application termination.
- **Concurrency**: Go handles each request in a new goroutine, allowing for concurrent processing.
- **Default Behavior**: By default, Go unwinds the stack, calls deferred functions, and logs the stack trace leading to the panic.
- **HTTP Impact**: A panic in an HTTP request closes the underlying HTTP connection, not the entire application.
- **Middleware Recovery**: Middleware can be used to recover from a panic and provide a more informative response.
- **Connection Header**: If a panic occurs, set the connection header to closed.
- **HTTP/2 Note**: In HTTP/2, the Go HTTP server automatically closes the connection after the response due to the header's connection being set to closed.

- A panic automatically closes a http connection, however, *manually setting the connection header to closed in middleware can be useful for a couple of reasons:*
	1. The connection will automatically be terminated after the response it sends. 
	2. It informs the user that the connection will be closed. 


