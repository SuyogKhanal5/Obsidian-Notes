- ### Repetition
	- ###### Consider Repetition!
		- If one event with $n$ outcomes occurs $r$ times with repetition allowed, then the number of ordered arrangements is $n^r$
		- Examples
			- What is the number of arrangements if a die is rolled 2 times?
				- $6 \cdot 6 = 36$
			- What about 4 times?
				- $6^{4}$ times
			- How many different car number plates are possible with 3 letters followed by 3 digits?
				- $26^{3} \cdot 10^{3} = 17,576,000$
			- How may of these plates begin with ABC?
				- $1^{3} \cdot 10^{3} = 1,000$
			- How many ways can 6 people be arranged in a row?
				- Once we place the first person, we have 5 more options for the next, 4, 3, 2, 1. So our answer is $6!=720$
			- How many arrangements are possible if only 3 are chosen?
				- We have 6 options for the first one, 5 for the second, 4 for the third, and then no more generators, so the answer is $6 \cdot 5 \cdot 4 = 120$
	- ###### Ex. How many ways to assign 100 passengers to 20 first class seats?
		- $n = 100$, we are choosing $k=20$ seats
		- Order matters, so we are doing permutations, not repeating
		- $\frac{100!}{100! - 20!} = \frac{100!}{80!}$
	- ###### Ex. Have $n$ colors, and want to paint $k$ tiles. How many ways? Reuse allowed.
		- $k$ generators, repetition allowed
		- $n^k$ possible ways
	- ###### Ex. If 10 horses race, how many orderings of top 3 finishers are there?
		- 10 elements choose 3
		- $n=10$, $k=3$
		- Order is important
		- No repetition allowed
		- $\frac{10!}{7!}$ possible ways