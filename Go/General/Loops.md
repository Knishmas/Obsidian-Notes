## Range loops 
- Used to iterate over elements within data structures. 
- *Convenient* way to access elements without having to manage indices or keys . 
- **Arrays and Slices**: When used with arrays or slices range it returns 2 values. *Index*, and a copy of the *element* at said index. 
*Example*
```go
nums := []int{1, 2, 3, 4, 5} 
for i, num := range nums { 
	fmt.Printf("Index: %d, Value: %d\n", i, num) 
}
// Index: 0, Value: 1 Index: 1, Value: 2 Index: 2...
```

- **Strings**:  When used with strings, `range` returns the *index* and the *Unicode* code point for each character in the string
- **Maps**:  When used with maps, `range` returns a **key-value pair** for each entry in the map.
-