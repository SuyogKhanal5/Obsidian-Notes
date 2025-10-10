
- ### Conditional Probability
	- Additional information
	- Conditional on, given that, if …
	- ###### Calculating Conditional Probability
		- $P(B|A)=\frac{P(AB)}{P(A)}$
		- Ratio of joint probability and marginal probability
		- Use when numerator is easy to calculate

- ### Rule of Elimination
	- ###### Rearrange conditional probability formula
		- $P(AB)=P(A)P(B|A)=P(B)P(A|B)$
		- Called multiplicative rule of probability
	- ###### Rule of Elimination
		- If event $B_{1},B_{2},\dots B_{k}$ constitute a partition of the sample space, it means
			- $B_{i}$ are mutually exclusive and $P(B_{i})\ne 0, \sum P(B_{i})=1$
			- Then $P(A)=\sum P(A \cap B_{i})=\sum P(B_{i})P(A|B_{i})$![[Pasted image 20250905085523.png]]

- ### Bayes Theorem
	- $k$ mutually exclusive events: $\sum_{i}P(B_{i})=1$
	- An observed event $A$: $P(B_{i}|A)=\frac{P(B_{i}\cap A)}{P(A)}=\frac{P(B_{i})P(A|B_{i})}{\sum_{i}P(B_{i})P(A|B_{i})}$
	- ###### When to use
		- You are given (or it is easy to get)
			- $P(B)$: The prior
			- $P(A|B)$: The evidence
		- You are asked to solve
			- $P(B|A)$: The posterior
	- No need to memorize formula, use tree diagram

