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