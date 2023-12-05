# Minimum

_Instructions: write a `min` function that takes two parameters and returns the minimum_

_Solution_

```javascript

const min = (min1, min2) => {(
    if(min1 < min2){
        return min1;
    }else{
        return min2;
    }
)}

const testCase1 = min(1,2);
const testCase2 = min("Cofee","Apple fritters");
const testCase3 = min(3,2);

console.log(testCase1, testCase2, testCase3);

```

# Recursion

_Intructions: We’ve seen that % (the remainder operator) can be used to test whether a number is even or odd by using % 2 to see whether it’s divisible by two. Here’s another way to define whether a positive whole number is even or odd:_

_Zero is even._

_One is odd._

_For any other number N, its evenness is the same as N - 2._

_Define a recursive function isEven corresponding to this description. The function should accept a single parameter (a positive, whole number) and return a Boolean._

_Test it on 50 and 75. See how it behaves on -1. Why? Can you think of a way to fix this?_

_Solution_

```javascript
const isEven = (N) => {
  if (N < 0) return false;
  if (N === 1) return false;
  if (N == 0) return true;
  return isEven(N - 2);
};

for (let i = 50; i < 75; i++) {
  console.log(`${i} is: ${isEven(i)}`);
}

console.log(`-1 is: ${isEven(-1)}`);
```

# Counting Beans

_Write a function `countBs` that takes a string as its only argument and returns a number that indicates how many uppercase “B” characters there are in the string._

_Solution_

```javascript
const countBs = (input) => {
  //-1 denoting invalid input
  if (typeof input != "string") return -1;
  let bCount = 0;
  for (let i = 0; i < input.length; i++) {
    if (input[i] === "B") bCount++;
  }
  return bCount;
};

console.log(countBs("This has two B's in it. B"));

console.log(countBs(4));
```

_Next, write a function called `countChar` that behaves like countBs, except it takes a second argument that indicates the character that is to be counted (rather than counting only uppercase “B” characters). Rewrite countBs to make use of this new function._

_Solution_

```javascript
const countChar = (input, charVal) => {
  if (typeof input != "string") {
    console.log("1st parameter input must be of type string! Invalid input!");
    return -1;
  }
  if (typeof charVal != "string") {
    console.log("2nd parameter input must be of type string! Invalid input!");
    return -1;
  }

  let charCount = 0;
  for (let i = 0; i < input.length; i++) {
    if (input[i] === charVal) charCount++;
  }
  return charCount;
};

console.log(countChar("Test input T,T,T", "T"));
console.log(countChar(1, "T"));
console.log(countChar("Test input T,T,T", 4));
```
