
- ### Lists
	- Mutable, ordered sequence of elements
	- Indexable, sliceable, appendable, etc.
	- ###### Slicing
		- Extract a "slice" of a list by specifying a range
		- `list[start:end:step]`
		- `start` - Index to begin, inclusive
		- `end` - Index to stop slicing, exclusive
		- `step` - Number to step by, optional
		- Omit the start to start from the beginning, omit the end to go till the end, omit the step to step by 1
		- You can use negative numbers for the indexes to go backwards
			- Ex. `my_list[-2::-1]` Slice from second to last element to the beginning