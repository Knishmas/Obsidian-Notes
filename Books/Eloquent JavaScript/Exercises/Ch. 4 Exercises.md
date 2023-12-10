## The Sum of a Range
**Task**
*Write a `range` function that takes two arguments, `start` and `end`, and returns an array containing all the numbers from `start` up to (and including) `end`.*

*Next, write a `sum` function that takes an array of numbers and returns the sum of these numbers. Run the example program and see whether it does indeed return 55.*

**Solution**
```javascript
const range = (start,end) =>{
    let rangeArray = [];
    for( i = start; i <= end; i++){
        rangeArray.push(i);
    }
    return rangeArray;
}

//Bonus
/* -----------------------------------------------
//Optional parameter with a default values to handle ascending and descending range values
const range = (start, end, step = start < end ? 1 : -1) => {
  let rangeArray = [];
    //Positive step: Incrementing up the given range
    if(step > 0){
        for(i = start; i <= end; i+= step){
            rangeArray.push(i); 
        }
          //Negative step: Decrementing down the given range
    }else{
         for(i = start; i >= end; i+= step){
            rangeArray.push(i); 
        }
    }
    return rangeArray;
}
----------------------------------------------- */

const rangeArray = range(1,10)
console.log('This is the range array:' + rangeArray);

const sum = (...numbers) => {
    let total = 0; 
    for( let number of numbers ){
        total += number; 
    }
    return total; 
}

console.log('This is the sum of the range array:' + sum(...rangeArray));
```


**Reverse an array**

```javascript 
const reverseArray = (arrayInput) => {
    let reversed = [];
    const lastIndex = arrayInput.length -1; 
    
    for(let i = lastIndex; i >= 0; i--){
        reversed.push(arrayInput[i])
    }
    return reversed;
}

const reverseInPlace = (arrayInput) => {
   let left = 0; 
   let right = arrayInput.length - 1; 
   
   while(left < right){
       let temp = arrayInput[left]; 
       arrayInput[left] = arrayInput[right]; 
       arrayInput[right] = temp; 
       left++; 
       right--; 
   }
   return arrayInput; 
}


console.log(reverseArray([1,2,3,4,5]));
console.log('reversed in place:' + reverseInPlace([1,2,3,4,5]));
``` 

**A List**
*Task*
- *1. Write a function `arrayToList` that converts an array into a list.*
- *2. Write a function `listToArray` that converts a list into an array.*
- *3. Write a helper function `prepend` that adds an element to the front of a list.*
- *4. Write a helper function `nth` that returns the element at a given position in a list.*

```javascript
const arrayToList = (arr, obj, index){ 
	if(index === array.length - 1) return null; 
	obj.val = arr[index]; 
	obj.rest = arrayToList(array, obj.rest, index + 1); 
	return obj; 
}

const listToArray = (obj, arr) => { 
	if(obj == null) return arr; 
	arr.push(obj.value); 
	return listToArray(obj.rest,arr); 
}

const prepend = (element, list) => { 
	return {value: element, rest: list} 
} 

const nth = (list, n) => {   
	if (!list) return undefined;  
	else if (n == 0) return list.value;  
	else return nth(list.rest, n - 1);
}
```

**Deep Comparison**
*Task: Write a function deepEqual that takes two values and returns true if they are the same value or objects with the same properties, where property values are equal when compared with a recursive call to deepEqual. Use the typeof operator to determine if values should be compared directly or if their properties should be compared, and Object.keys to iterate over object properties.*
```javascript 
const deepEqual = (obj1, obj2) => {
	// Check if obj1 and obj2 are the same object
	if (obj1 === obj2) return true; 
	// Check if obj1 and obj2 are both objects
	if (typeof obj1 !== 'object' || obj1 === null || typeof obj2 !== 'object' || obj2 === null) return false; 
	// Check if obj1 and obj2 have the same number of properties 
	let keys1 = Object.keys(obj1); 
	let keys2 = Object.keys(obj2); 
	if (keys1.length !== keys2.length) return false; 
	// Check if corresponding properties of obj1 and obj2 are equal 
	for (let key of keys1) { 
		if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key]))return false; 	
	} 
	return true; 
};

```