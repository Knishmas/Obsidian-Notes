**Abstraction:** Hide details and be able to talk about problems at a higher level.

## Abstracting Repetition
- We can create functions to abstract repeated code. It will be much cleaner. 
- *Note: You don't always have to create a predefined function to repeat. Sometimes it's easier to create the `func` on the spot.* 

## High-Order Functions
- **Functions that utilize other functions by taking them in as arguments or returning them.** 
- Allow us to abstract over *actions* and not just values. In several ways.
	- Functions that create new functions. 
	- Functions that change other functions 
	- Functions that provide new types of control flow.

*Example*
```javascript 
function greaterThan(n) {
  return m => m > n;
}
let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11)); // → true
```
- We're returning an *action* and setting it to a variable to be called as a function. 