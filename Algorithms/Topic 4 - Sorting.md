- # PROVE ALGORITHM CORRECTNESS IDK WHERE THIS IS BUT I NEED TO LEARN

- ### Randomized Quick Sort
	- Choose a pivot element at random.  
		- By choosing a pivot element at random, we minimize the chance of a worst case partition
	- Partition the array into three subarrays containing the elements smaller than the pivot, the pivot element itself, and the elements larger than the pivot.  
	- Recursively quicksort the first and last subarrays.

- ### Comparison Based Sorting
	- Any comparison based sorting algorithm requires $n \log n$
		- If $k$ steps are required we see that we need $2^k$ should at least $n!$ to get all possible output of sorted lists
		- $k \ge \log n! = \Theta(n \log n)$

- ### Counting Sort
	- The first step of the algorithm initializes the array $C$, in $O(M)$ time
	- Next, the second step involves iterating through all the elements, requiring $O(n)$ time
	- In the third and fourth steps, the total time complexity is $O(n+M)$. This is  because each iteration of the for-loop increments $j$ by $1$, and $j$  can only increase up to $M$ times. Similarly, the while-loop  increments 𝑝, but 𝑝 can only increase up to 𝑛 times overall.  
	- Therefore, the total runtime of the algorithm is $O(n+M)$

- ### Heap Sort
	- Time complexity: $O(n \log n)$
	- Steps:
		- Build Min-Heap from array: $O(n)$
		- Repeated extract the smallest element from the heap, store in new array: $O(\log n)$ per element
	- ###### Sorting a k-Sorted Array
		- An array is **k-Sorted** if every element is at most $k$ positions away from its correct position
		- Algorithm:
			- Build Min-Heap from the first $k+1$ elements
			- For each element in the array, extract the minimum and insert the next element
		- Total Complexity: $O(n \log k)$, better than $O(n \log n)$ if $k < n$

- ### Greedy Algorithms
	- Locally good choices (typically very bad)
	- Most greedy algorithms don't work, therefore need a proof of correctness