# 3.3 Dependency Injection 
*How can we make dependencies available?*
- **Best Practice:** Inject dependencies. 
	- Makes code more explicit, less error prone, and easier to unit test rather than using global variables. 
	- For applications with handlers all in the same file, a convenient way to inject dependencies is through creation of custom application structs.


# Side notes
- If you are creating a struct method and you want to alter an object, you need to make sure the method has a pointer receiver to the object in order to make an actual change to the object. Other wise if you just pass the object, go will change a copy of the object that is local to that method. 
