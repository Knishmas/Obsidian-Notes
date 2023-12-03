- **Correlation:** a statistical measure of relation between two variables.
	- Usually expressed as values from: -1 to 1
	- where 0 is unrelated. 
	- 1 is a perfect relation 
	- -1 is perfectly related, but opposites (true and false)
-  **Phi coefficient (ϕ):** A measure of association for two binary variables.
- **.includes()** : Method for arrays to check if item exists in it. Returns Boolean.
- `push()` & `pop()`: adds and removes items at the end of an array.
- `unshift()` & `shift()`: Adding and removing items at the beginning of the array. 
	- Unshift adds, shift removes. 
	- Can make queue out of an array with these two methods. 
- `indexOf()` Searches start to end of an array for an item and returns it's index or -1 if not found. 
- `lastIndexOf`: returns the last index of found item. Example [1,2,3,2] returns 3.
- Note: Both index functions have an optional 2nd parameter which determines where the search starts.
- `slice()`: Takes the start and end positions of an array and returns only the items b/w them. 
	- End index can be omitted and all the elements after the start will be included. 
	- The start index can be omitted with the end and it will copy the entire array. 
	- Example: .`slice(2,4) [0,1,2,3,4] -> 3
	- Example: .`slice(2) -> [3,4]
`.concat()`: Create two arrays as one. Imagine glue'ing them together.
*Example*
```javascript 
var arr1 = [1, 2, 3]; 
var arr2 = [4, 5, 6]; 
var arr3 = arr1.concat(arr2); 
console.log(arr3); // [1, 2, 3, 4, 5, 6]
```
- *Note:* if you push an element that isn't an array to concat() then it will push that item into the array like it was a single element array. 

## Strings & their properties

- Values of type string, number, and Boolean _are not objects_. Although they do have properties, properties which are _immutable and cannot change_.
- For example String has the `.length` & `toUpperCase` property, but if you try to add new properties nothing will happen.
_Example_
```javascript 
let kim = "Kim";  
kim.age == 88; 
console.log(kime.age); 
// -> undefined
```

- Some string properties are: `slice(), indexOf(), time(), padStart(), join(), & repeat()`.

## Array Loops 
- Traditional for i...
```javascript
for(let i = 0; i < JOURNAL.length; i++){
	let entry = JOURNAL[i];
}
```
- Simplified modern for every item...
```javascript
for( let entry of JOUNRNAL){
	console.log("found journal entry")
}
```

## Rest Parameters 
- **Rest function**: A function in which is able to take in any number of arguments utilizing the `...` syntax. (placed before)
*Example*
```javascript 
function max(...numbers){
	... 
	//Takes the maximum number of all the inputs. 
}
	console.log(max(4,1,9,-2))
	//output: 9
```
- *Note: when the rest function is called, the rest parameter is bounded to an array of the arguments. If there's other parameters before it, they won't be part of the array.*
- You can use the same `...` notation to call an array of arguments to the rest function
```javascript
let numbers = [5,1,7]
console.log(max(...numbers))
//Output: 7 
```

## The Math object 
- Acts as a namespace for various related functions that *don't have global bindings*. 
*Why is it beneficial that all of its content is within an object and not globally binded?*
- Too many globally binds can *pollute* the space and you're more likely to overwrite variables the more global bindings you have.  
*Example*: You want to write a var max, since JavaScript's max is tucked into the Math object it won't be overwritten.
- Javascript will warn you if you are defining a binding with a name that's already taken, but only for `let` & `const` not with `var` & `func()`. 
- The Math object contains: `PI` ,`cos`, `sin`, `tan`, & their inverses. 

## Destructing 
- Allows you to unpack values from arrays or properties from objects into distinct variables. 
- The benefit to this is that it makes code cleaner and easier to read. 

- **Array Destructuring**
```javascript
const date =['1970', '12', '01']
const [year, month, date] = date; 
console.log(year); // 1970
console.log(month); // 12
console.log(date); // 01
``` 

 **Object Destructuring** 
 ```javascript
const note = {
	id: 1, 
	title: 'First note',
	date: '01/01/1970',
}; 

const {id, title, date} = note; 
console.log(id); // 1
console.log(title); // "First note"
console.log(date); // "01/01/1970"
```

**Nested Destructuring**
- You can also destructure nested arrays and objects. 
```javascript 
const nestedArray = [1,2, [3,4], 5]
const [one, two, [three, four], five] = nestedArray;
console.log(one,two,three,four,five)// 1,2,3,4,5
```

**Rest Parameter(...) Destructuring**
```javascript 
const baz = ["one", "two", "three", "four"]; 
const [a,b, ...rest] = baz; 
console.log(a); //one
console.log(b); //two
console.log(c); // ["three", "four"]
```

**Using destructuring with functions**
*Example*
```javascript 
function sum([a,b]){
	return a + b; 
}

let numbers = [1,2]
console.log(sum(numbers)) // 3
```
