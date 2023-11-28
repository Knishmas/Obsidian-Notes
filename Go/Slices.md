- Similar to an array list in which it acts like a dynamic array. 
- When we create an array in go, it has to have a pre-determined size and it stays at that size. This is where slices are beneficial. 
- Slices are their own data type/

## Arrays 
*Arrays are represented by 3 things in Go*
- **Pointer**: The location of the first element in the array
- **Length & Capacity**: Tell us how many elements are in the array. 

- **Length**: The # of elements in the array.
- **Capacity**: The max amount of elements we can have.
*Note: The length and capacity of arrays in go are always the same.*

## Slices
- **Slice**: A portion of an array.
- Their own data type. 
- A slice is represented like an array with some key difference. 
	- **Pointer**: The location of the first element in the slice, but the location is the location of whatever element is in that *underlying array.*
	- Unlike arrays, length and capacity within slices are *different*. 
	- **Length**: The number of elements in the slice. 
	- **Capacity**: How many elements in total we could have. This includes if we extended the slice after it's current endpoint, if it has any space available. 

*Example*
- [0,[6,3],9]
	- [0,6,3,9] is our array 
	- [6,3] is a slice of that array.
	- The length of the slice is 2. 
	- The capacity of the slice is 3 because we have an additional space we can extend it by within the original array. It could be expanded from [6,3] -> [6,3,9 ]  

- Creating a slice 
*Example*
```go 
var x [5]int = [5]int{1,2,3,4,5,}
var s []int = x[1:3]
// s = [2,3] length = 2, capacity = 4
```
- If you don't include a capacity when you declare an array, it becomes a slice. 
- To create a slice from an array you can utilize `:` and include the range of elements you'd like to take a slice from (endpoint is non-inclusive). If it isn't specified then it will take a slice from the beginning of the array to the end. 

- We can *re-slice* slices if we wanted to.
*Example: 
```go
s[:cap(s)]
//Extends the slice of s to it's full capacity: [2,3,4,5]
```


- Shorthand way of creating a slice
```go 
var a []int = []int{5,6,7,8,9}
//Creates an array and then takes a slice of it all. 
```
- `append()`: Allows you to append to slices.
	- Takes 2 parameters: The slice and what you want to append. 
	- Returns a new slice that includes the appended value. 
```go 
b := append(a,10)
// b = [5,6,7,8,9,10]
```
- `make()`: Creates an empty slice of a specific size. 
	- Takes 2 parameters: slice type and size. 
```go 
a := make([]int, 5)
// a = [0,0,0,0,0]
//Creates an empty integer slice of size 5. 
```