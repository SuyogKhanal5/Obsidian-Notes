
- ### Induction
	- Let $P(m)$ be a predicate of non-negative integers
	- You want to prove that $P(m)$ is true for all non-negative integers
	- Step 1: Prove that $P(0)$ is true (the base case)
	- Step 2: Prove that $P(n) \Rightarrow P(n+1)$, $\forall n \notin \mathbb{Z}^-$

- ### Counting
	- Basic Question: What is the size of a given set?
	- Easy when the set is explicitly defined?
		- $X=\{1,2,3,4\}$, what is $|X|$
	- Tricky when set is implicit or a defined via set operations
		- How many ways to get flush in a game of poker?
		- How many operations before my algorithm terminates

- ### Sum Rule
	- ###### **Sum Rule**: If $A_{1}, A_{2}, ..., A_n$ are **disjoint** sets, then:$|A_{1} \cup A_{2} \cup \dots \cup A_{n}| =|A_{1}| + |A_{2}| + \dots + |A_{n}|$
	- Ex. There are 60 students in section 5 of CS206, there are 71 students in sections 6 of CS206, how many students are there in total in both sections? 131 students, since there is no overlap between the two sets (disjoint sets).

- ### Partition Method
	- ###### To find the size of a set $A$
		- Partition it into a union of disjoint sets $A_{1}, A_{2}, ..., A_{n}$
		- Use sum rule
	- ###### Ex. If I roll a white die and a black die, how many possible outcomes do I see? 
		- $S=$ $\begin{Bmatrix}(1,1) & (1,2) & ... & (1,6) \\ (2,1) & (2,2) & ... & (2,6) \\ \vdots & \vdots & \ddots & \vdots \\ (6,1) & (6,2) & ... & (6,6) \end{Bmatrix}$
		- $A_{1} =$ all outcomes with black die $=1$
		  $A_{2}=$ all outcomes with black die $=2$
		   $\vdots$
		 $A_{6}=$ all outcomes with black die $=6$
		- $|S| = |A_{1}| + |A_{2}| + \dots + |A_{6}| = 6 \cdot 6 = 36$
	- ###### What about the possible outcomes where the dies both have different values?
		- $A_{1} =$ all outcomes with black die $=1$
		  $A_{2}=$ all outcomes with black die $=2$
		   $\vdots$
		 $A_{6}=$ all outcomes with black die $=6$
		- $|A_{1}|=5, |A_{2}| = 5$
		- $|S|=5+5+5+\dots+5=30$

