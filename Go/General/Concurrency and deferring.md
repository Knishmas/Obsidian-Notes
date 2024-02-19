# Defer 
```go 
func main() { 
	defer fmt.Println("world") 
	fmt.Println("hello")
 }
 /*
 output: 
	 hello 
	 world
*/
```
- When functions are deferred, they're put onto a stack. 
- When a panic occurs the function exits and unwinds the stack calling the deferred functions in order of last in first out. 

```go 
func main() {
 defer fmt.Println("cleaning up") 
 fmt.Println("starting main") 
 panic("an error occurred") 
 fmt.Println("ending main") 
 }
  /*
 output: 
	 starting main 
	 cleaning up
	 panic: "an error occured"
*/
```
- The panic message will get printed last after all deferred functions have been called. 