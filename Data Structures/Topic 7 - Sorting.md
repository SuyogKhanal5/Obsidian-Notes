
- ### Selection Sort
	- Most basic sorting method, find the smallest element and add it to the start![[Pasted image 20231007191809.png]]

- ### Insertion Sort
	- Iterate through the unsorted array, and then for each new element you encounter place it in sorted order with the ones you have already seen![[Pasted image 20231007191638.png]]
	- Time Complexity: $O(n^2)$
	

- ### Quicksort
	- **Split**: Select a pivot element, and split an array in two subarrays based on the pivot
		- All elements less than the pivot are put in the left array
		- Pivot and the elements greater are put in the right array
	- Then calls itself recursively twice to sort the two sub arrays
	- Time Complexity: $O(n\log(n))$
	- ```quicksort(a, left, right)
		  if (right <= left) return;
			split(a, left, right)
			quicksort(a, left, splitPoint-1)
			quicksort(a, splitpoint+1, right)```
- ### Mergesort
	- Split into subarrays recursively and sort as you put the array back together![[Pasted image 20231007191350.png]]
	- Time Complexity: $O(n\log(n))$