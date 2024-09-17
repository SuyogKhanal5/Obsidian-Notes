
- ### Dictionaries
	- Collection of key value pairs
	- Unique immutable keys
	- Values can be any python object
	- ###### Methods
		- `dict.get(key)`
			- Gets value for specified key
		- `dict.keys()`
			- Returns view object that displays all keys
		- `dict.values()`
			- Returns view object for all values
		- `dict.items()`
			- Returns view object for all key value pairs

- ### Sets
	- Unordered collection of unique elements
	- Defined with $\{\}$ or `set()`
	- To easily remove duplicates from a list, cast set onto it
		- `no_dups = set([1,2,2,3,4])`
	- ###### Set Operations
		- **Union** ($|$) - Combine elements from both sets
		- **Intersection** (&) - Return elements that are in both sets
		- **Difference** ($-$) - Return elements in one set that are not in the other
		- **Symmetric Difference** (^) - Return elements in either set but not both

- ### List Comprehension
	- Works for sets and dictionaries too
	- List: `[x**2 for x in range(5)]`
	- Dictionary: `{x : x**2 for x in range(5)}`
	- Set: `{x**2 for x in range(5)`

- ### Performance Considerations
	- Tuples are faster than lists for read only operations
	- Sets and Dictionaries ideal for quick lookup
