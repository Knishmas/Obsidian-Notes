- **Interface:** Similar to a definition that defines the exact methods another type has.
- A *interface* defines actions that a type must be able to perform. If the type can perform all of the interface's actions, then it is said to *follow the interface.*
- A benefit to interfaces is that you're able to write code that works with any type, without even knowing it, so long as it follows the interface. 

*Example*
*We have a `Playable()` interface that requires a button to have a `PressButton()` method.*
```go 
type Playable interface {
  PressButton() string
}
```

- Now let's say that we have 2 types of toys: RobotToy & DollToy each with a `PressButton()` function 
- We can now write a function that plays with any toy that follows the `Playable` interface. 
```go 
func main() {
  robot := RobotToy{}
  PlayWith(robot) // prints "Beep!"

  doll := DollToy{}
  PlayWith(doll) // prints "Hello!"
}
```

**Summary:** an interface in Go is like a rule that a type must follow. It allows you to write code that can handle many different types in the same way, as long as they follow the rules defined by the interface. 

- Notes: 
- Go implicitly implements a type to an interface, you don't need to explicitly declare it as such. 
- As long as a type contains ALL the methods of an interface it will implement it. A type can have more methods beyond the ones required for it to implement an interface and it will still implement it.
- It's possible for a type to implement multiple interfaces. 