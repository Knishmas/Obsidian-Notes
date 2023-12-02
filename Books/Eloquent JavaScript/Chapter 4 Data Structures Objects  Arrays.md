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
