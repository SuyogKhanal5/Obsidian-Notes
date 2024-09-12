
- ### Criteria For Analysis
	- Accuracy, Proof of Correctness
	- Time Complexity
	- Space Complexity
	- Best-Case, Average-Case, Worst-Case
	- Optimality (lower and upper bounds)
	- Amortized Analysis
	- Approximation, Probabilistic guarantees

- ### Euclid's Algorithm and Proof of Correctness
	- Developed by Euclid to find the gcd of two numbers
	- ```def gcd(a, b)
		if b == 0:
			return a
		else:
			return gcd(b, a % b) ```
	- ###### PROOF OF CORRECTNESS
		- Base Case:
			- If $b = 0$ the algorithm returns $a$
			- $\text{gcd}(a,0)=a$ since any number divides $0$
		- Inductive Step:
			- $d$ divides $a$ and $b$ $\Leftrightarrow$ $d$ divides $a$ and $a$ $\text{mod}$ $b$
			- $\therefore$ $\text{gcd}(a,b)=\text{gcd}(b,a$ $\text{mod}$ $b)$
			- In each recursive call $b$ becomes smaller and the recursion continues until $b=0$
			- The algorithm terminates when $b=0$ ensuring correctiveness
	- ###### Number of Iterations
		- The sum of the variables $a+b$ decreases by a factor of at least $\frac{3}{2}$ every iteration
		- Let $a=bq+r$ and $0 < r < b$ such that $r = a$ $\text{mod}$ $b$. Note that $q \ge 1$ since $a > b$
		- The sum after one iteration is $b+r$ and we have $3(b+r) = 2(b+r) + b + r$
		- This is less than $2a + b + b = 2(a+b)$
		- $\therefore$ The number of iterations is at most $\log_{\frac{3}{2}}(a+b)$

- ### Time Complexity
	- ###### How do we measure the running time of an algorithm?
		- Experiments: Plot the run times for various input sizes
		- Experiments need actual implementation and use limited inputs
		- Comparing two algorithms needs same software and hardware environment
		- We instead compare the number of primitive operations that need to be executed for in some model of computation
		- Look at the asymptotic growth rate
		- Assume the worst case
	- ###### Model of Computation
		- We will use the RAM (Random Access Machine) model of computation
		- A simple operation (e.g. $+,-,*,=,\text{if}$) takes exactly *one* time step
		- Loops and subroutines are built from simple operations and their runtime is the sum of the steps of those operations
		- *Memory Access* is unlimited and takes one step regardless of whether it is stored in cache, RAM, or on disk
		- The running time is measured by counting the *number of steps* an algorithm takes for a given input
	- ###### RAM vs Real Machines
		- Limited Memory: Access is constrained by physical memory and word sizes
		- Hierarchical Memory: Includes registers, L1/L2 caches, and main memory with different access times. 
		- Memory Latency: Memory access may take multiple cycles depending on where data is (cache or RAM)
		- Pipelining vs Superscalar Execution: Multiple instructions ($1-4$ or more$)$ may be executed in a single CPU cycle
		- Memory Bottleneck: Data movement between registers and memory can create delays
		- Branch Prediction: Modern CPUs guess the outcome of branches to optimize execution
		- Parallelism: Modern architectures support parallel execution (multithreading)
		- ***Example***
			- `x=y+z`
			- This statement takes one step in RAM
			- In a real machine the `y` and `z` will be loaded to registers and then added to `x`
	- ###### Asymptotic Notation
		- **Big-O** $(O)$: Upper bound. $f(n)=O(g(n))$ if $f(n) \le c \cdot g(n)$ for some $c>0$ and large $n$
		- **Omega** $(\Omega)$: Lower bound. $f(n)=\Omega(g(n))$ if $f(n) \ge c \cdot g(n)$ for some $c>0$ and large $n$
		- **Theta** $(\Theta)$: Tight bound. $f(n) = \Theta(g(n))$ if $c_{1} \cdot g(n) \le f(n) \le c_{2}\cdot g(n)$ for some $c_{1},c_{2}>0$ and large $n$
		- **Little-O** $(o)$: Strict upper bound. $f(n)=o(g(n))$ if $\lim_{n\to\infty} \frac{f(n)}{g(n)}=0$
		- **Little-Omega** $(\omega)$: Strict lower bound. $f(n)=\omega(g(n))$ if $\lim_{n\to\infty} \frac{f(n)}{g(n)}=\infty$![[Pasted image 20240905145909.png]]