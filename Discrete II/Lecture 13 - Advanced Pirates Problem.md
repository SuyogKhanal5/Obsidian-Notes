
- ### When not to use combinations with repetitions?
	- The ability for some element to be size $0$ or size $n$ allows us apply the formula $${n + r - 1 \choose n-1}$$ If we are unable to choose $0$ or $n$ of an element, this formula is non applicable 

- ### Permutations and Combinations Flowchart![[Pasted image 20231029215526.png]]

- ### Advanced Pirates Problems
	- ###### $5$ pirates want to divide $20$ bars of gold among them. How many ways to divide if each pirate wants at least $2$ bars, and no pirate can get more than $8$ bars
		- Essentially the problem is $$x_1+x_2+x_3+x_4+x_5=20\text{ for }2 \le x_{i}\le 8$$
		- First give each of the pirates $2$ bars, which means we subtract $5 \cdot 2$ from $10$ $$x_1+x_2+x_3+x_4+x_5=10\text{ for }0 \le x_{i}\le 6$$
		- Consider that when counting the different ways to place our dividers among our gold bars, the constraint will invalidate some sequences
			- The invalidation of some elements means we can use the *difference method* to remove the sets of invalid sequences
			- Count all of the possible ways to divide $10$ bars among $5$ pirates, then subtract the number of ways in which some pirate gets more than $6$ bars
		- There are ${14 \choose 5}$ ways to divide $10$ bars among $5$ pirates
		- Consider that for some $x_{i}> 6$, only ONE pirate can get $6$ or more bars ($7x \le 10$ has only one integer solution, $x=1$), so either $x_1,x_2,x_3,x_4$ or $x_5$ will get more than $6$ bars
		- Lets use *partition method* to find how many ways a pirate can get more than $6$ bars of gold
			- There are $5$ ways for a pirate to get more than $6$ bars of gold
				- All ways to distribute so that pirate $x_1$ gets more than $6$ bars
					- Give $x_1$ $7$ bars, distribute the remaining $3$ among the rest $$x_2+x_3+x_4+x_5=3$$
					- We have $3$ gold bars and $4$ dividers, so ${7 \choose 4}$
				- All ways to distribute so that pirate $x_2$ gets more than $6$ bars
				- All ways to distribute so that pirate $x_3$ gets more than $6$ bars
				- All ways to distribute so that pirate $x_4$ gets more than $6$ bars
				- All ways to distribute so that pirate $x_5$ gets more than $6$ bars
			- $5\cdot {7 \choose 4}$
		- So, ${14 \choose 4} - 5\cdot {7 \choose 4}$
