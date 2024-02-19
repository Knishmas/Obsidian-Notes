- **Methods** are functions that are associated with a specific type. They have an extra parameter, the receiver, which enables the method to access the properties of the receiver. The receiver appears between the `func` keyword and the name of the method.

*Example*
```go 
type Circle struct {
  Radius float64
}

func (c Circle) Area() float64 {
  return math.Pi * c.Radius * c.Radius
}
```
- Methods and interfaces are similar in the fact that they operate on types, however they are different 
- Methods are associated with a type and can operate on an instance of that type, while interfaces define a contract of methods that a type must fulfill.