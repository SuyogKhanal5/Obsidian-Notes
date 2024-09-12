
- ### Python vs. Java
	- Dynamically typed
	- Indentation based
	- Interpreted, not compiled
	- Slower
	- Both have automatic garbage collection
	- Limited multithreading support
	- Cross platform via interpreter vs Cross platform via JVM
	- Used for Web Dev, Data Science, Scripting
	- Simpler syntax
	- Procedural and Object Oriented vs Fully Object Oriented

- ### Type Safety
	- Type is inferred at runtime
		- More flexible, but error prone
	- **Polymorphism** - Functions can operate on objects of different types as long as they have compatible attributes or methods![[Pasted image 20240909180256.png]]

- ### Garbage Collection
	- Variables are references to objects, so if the original object no longer exists or no references to object exist the garbage collection will set the variable to `None` and free the memory ![[Pasted image 20240909180544.png]]

- ### Mutability vs Immutability
	- In python, lists are mutable, but strings are immutable
	- An object is **Mutable** if it can be changed after its creation
		- Mutable: List, Dictionary, Set
		- Immutable: Integer, String, Tuple
	- Variables can be reassigned but the original objects mutability determines if it can be changed in place or not

- ### Scope of Variables
	- Four types, Local < Enclosing < Global < Built-in
	- Python has dynamic scoping in function definitions, where variables are accessible in the functions they were created in
	- Variables defined inside function unless marked as global or non-local

- ### Explicit Declaration
	- No need for explicit declaration
	- Variables can be assigned anywhere without prior declaration or initialization, exists as soon as it is given a value