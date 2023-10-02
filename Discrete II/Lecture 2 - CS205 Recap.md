
- ### Combinatorics
	- The study of arrangements of objects
	- Studied as long ago as the 17th century, when combinatorial questions arose in the study of gambling games
	- Used to study many problems, such as:
		- **Enumeration** - The counting of objects *with certain properties*
			1. Counting determines the complexity of algorithms
			2. Counting determines whether there are enough resources to solve a problem
			3. etc.
	- It is also considered to be the study of discrete structures
		- We count structures of a given kind/size
			- What is the runtime complexity of an algorithm?
			- Do we have enough memory?
	- When we do a google search, we are given the amount of time the search took, and the number of results. We could never count the number of result manually, this is due to combinatorics. 
	- We will study the basic rules of counting
		- They can solve a tremendous variety of problems, such as:
			- Enumerate the **different telephone numbers** possible in the United States
			- Enumerate the **allowable passwords** on a computer system
			- Enumerate the **different orders** in which a the runners in a race can finish
		- They can help us answer questions that seem hard: *What is the chance that amount the 150 students in this class, we find 2 with the same birthday?*
	- An important combinatorial tool is the **pigeonhole principle**: When objects are placed in boxes and there are more objects than boxes, then there is a box containing at least 2 objects
		- We can use this to show the harder question above
	- How many passwords can we create given the following rules?
		1. Must be different from User ID
		2. Must contain 8 to 20 characters, including one letter and number
		3. May include %, &, \_, ?, #, =, -
		4. Password must be case sensitive and cannot have spaces
		- This question is able to be answered using Combinatorics

- ### Combinatorics leads to Probability Theory
	- **Probability Theory** - The analysis of uncertain or random phenomena 
	- The more information we have, the less uncertainty
	- As long as uncertainty exists, Probability Theory is needed

- ### Sets
	- ###### What is a set?
		- **Set** - A collection of objects called elements
		- **Elements** - Objects that share the same property
	- ###### Examples
		- Followers on Twitter
		- Set of webpages for a given Google query
		- Collection of YouTube videos
	- The order of the elements is not significant, so {$x,y$} and {$y,x$} are the same set
	- If $y=x$ then we have the set {$x,x$} which just becomes the set {$x$}
	- The expression $e \in S$ asserts the $e$ is an element of $S$
	- ###### Common Sets
		- $\emptyset$ - The empty set
		- $\mathbb{N}$ - The set of all Natural Numbers
		- $\mathbb{Z}$ - The set of all Integers
		- $\mathbb{Q}$ - The set of all Rational Numbers
		- $\mathbb{R}$ - The set of all Real Numbers
		- $\mathbb{C}$ - The set of all Complex Numbers
		- A superscript $^+$ restricts a set to its positive elements, same with $^-$ for negative elements
	- ###### Set Operations
		- $X \cup Y$ - **Union**: All elements present in $X$ or $Y$ or both
		- $X \cap Y$ - **Intersection**: All elements present in *both* $X$ and $Y$
		- $X \setminus Y$ - **Difference**: All elements present in $X$ but *not in* $Y$ 
			- Not Symmetric
		- $X \times Y$ - **Product**: Collection of all tuples ($a,b$) where $a \in X$ and $b \in Y$
		- $|X|$ - **Size**: Number of elements in $X$
	- ###### Set Comparisons
		- $X \subset Y$ - **Subset** - Every element present in $X$ is also present in $Y$
			- $X$ is **NOT** the same as $Y$
		- $X \supset Y$ - **Superset** - Every element present in $Y$ is also present in $X$ 
			- $X$ is **NOT** the same as $Y$
		- Note: There is a direct analogy between ($\subset$ and $<$) and ($\subseteq$ and $\le$)
	- ###### Power Set
		- Let $X$ be a set
		- Power($X$) is the set of all possible subsets of $X$
		- Ex. Power({$1,2$}) = {$1$}, {$2$}, {$1,2$} and $\emptyset$
		- Generally if $A$ has $n$ elements, then there are $2^n$ sets in Power($A$)
	- ###### Set Builder Notation
		- Often sets cannot be fully described by listing the elements explicitly or by taking unions, intersections, etc., of easily described sets
		- **Set Builder Notation** defines a set using a predicate, in particular the set consists of all values that make the predicate true
		- ###### Examples
			- $X = \{n \in \mathbb{N}$ | n is prime $\}$
			- $Y$ = {$x \in \mathbb{R}$ | $x^{3}-3x+1 > 0$}
			- $Z$ = {$z$ $\in$ YouTube Videos | $z$ is less than 3 minutes long}
	- ###### Exercise 1
		- Let $A$ = {$n \in \mathbb{N}$ | $n^{2}< 7$ } and $B = \{1,4,9\}$
		- So $A$ = {$0,1,2$}
		- Find
			- $A \cup B$ - {$0,1,2,4,9$}
			- $A \cap B$ - {$1$}
			- $A \times B$ - {$(0,1), (0,4), (0,9), (1,1) (1,4), (1,9), (2,1), (2,4), (2,9)$}
			- $A \setminus B$ - {$0, 2$}
	- ###### Venn Diagram
		- Represent circles as sets and dots as elements
		- Venn Diagram is able to represent unions, intersections, and differences easily
	- ###### Exercise 2:
		- There are 131 students in CS206
		- 100 like chocolate ice cream, 50 like vanilla ice cream
		- 20 like both chocolate and vanilla ice cream
		- Draw a Venn Diagram to represent this
		- $A$ is chocolate, $B$ is vanilla
		  ![[Drawing 2023-09-20 14.19.18.excalidraw|500]]
		- $|A| = 100$ like chocolate ice cream
		- $|B| = 50$ like vanilla ice cream
		- $|A \cap B| = 20$ like both
		- $|A \cup B| = |A| + |B| - (A \cup B)| = 130$ like chocolate, vanilla, or both
		- $131-|A \cup B| = 1$ student does not like either
		 

