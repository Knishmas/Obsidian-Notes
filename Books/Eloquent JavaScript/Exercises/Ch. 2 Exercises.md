# Loop a triangle 
*Intructions: Write a loop that makes seven calls to `console.log` to output the following triangle:*
```
#
##
###
####
#####
######
#######
```
*Solution* 
```javascript
let triangle = "#"
while(triangle.length != 8){
    console.log(triangle);
    triangle += "#"
}

```


# FizzBuzz
*Intructions: Print every number from 1-100. If divisible by 3 print out "Fizz". If divisible by 5 print out "Buzz". If divisible by both then print "FizzBuzz"*
```javascript
for(i = 1; i < 100; i++){
    if((i % 3) === 0 && (i % 5) === 0){
        console.log("FizzBuzz");
    }else if ((i % 3) === 0){
         console.log("Fizz");
    }else if ((i % 5) === 0){
         console.log("Buzz");
    }else{
        console.log(i);
    }
}

```

# Chessboard 
*Instructions: Write a program that creates a string that represents an 8x8 grid, using newline characters to seperate lines. At each position of the grid there is either a space or a # character. The characters should form a chessboard. Passing this string to console.log should show something similar to a chessboards representation. Allow it so that the input size is allowed to be changed.*

*Solution* 
```javascript

const createBoard = (size) => {
    let chessBoard = ""

    for(i = 0; i < size; i++){
        let startingChar = i % 2 ? " " : "#";
        if (i != 0) chessBoard += "\n"
        for(j = 0; j < size; j++){
            chessBoard += startingChar; 
            startingChar = startingChar === " " ? "#" : " "; 
        }
    }
    return chessBoard;
}

console.log(createBoard(16));


```
