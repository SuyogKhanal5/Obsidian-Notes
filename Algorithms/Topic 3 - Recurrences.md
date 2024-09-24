
- ### Merge Sort
	- ###### Time Complexity
		- Best case: $O(n \log n)$
		- Average case: $O(n \log n)$
		- Worst case: $O(n \log n)$
	- ###### Space Complexity
		- $O(n)$ (requires additional array)
	- ###### Recurrence
		- $T(n) = 2T(\frac{n}{2})+\frac{n}{2}$

- ### Expansion
	- Find the time complexity of the following recurrence: $T(n) = 2T(\frac{n}{2})+n$
	- Common in divide and conquer algorithms
	- Each problem is divided into 2 subproblems of size $\frac{n}{2}$
	- Additional work per level is linear: $\Theta(n)$
	- ###### Solve using expansion
		- $𝑇(𝑛) = 2 \cdot 𝑇(\frac{𝑛}{2}) + \Theta(n) = 2^{2}\cdot T(\frac{n}{2^2})+n+n$
		- $T(n)=2^{2}\cdot T(\frac{n}{2^2})+n+n$
		- $T(n)=2^3\cdot T(\frac{n}{2^3})+n+n+n$
		- $T(n)=2^{k} \cdot T(\frac{n}{2^{k}})+k \cdot n$
		- Stop when $\frac{n}{2^k}=1$, i.e $k=\log_2 n$
		- Substituting $k=\log_2 n$ gives us $T(n)=n+\log_2 n=O(n\log n)$

- ### Multiplication of Numbers
	- We want to multiply two large numbers $x$ and $y$, where each number is $n$ digits long. Traditionally this takes $O(n^2)$ time
	- We can split each number into two halves: 
		- $x=x_{1}\cdot 10^{\frac{n}{2}}+x_0$
		- $y=y_{1}\cdot 10^{\frac{n}{2}}+y_0$
	- The product $z=xy$ can be computed as follows:
		- $z=(x_{1}\cdot 10^{\frac{n}{2}}+x_0)(y_{1}\cdot 10^{\frac{n}{2}}+y_0)$
	- Expanding this gives us $z=x_{1}y_{1}\cdot 10^{n}+(x_{1}y_{0}+x_{0}y_{1}) \cdot 10^{\frac{n}{2}}+x_0y_0$
	- ###### Karatsuba's Algorithm
		- Reduces number of multiplications from 4 to 3
		- $z_{0}=x_{0}y_{0}$ and $z_{2}=x_{1}y_{1}$
		- We can directly compute $z_1=(x_1+x_0)\cdot (y_1+y_{0})-z_{0}-z_{2}$
		- $z=z_{2}\cdot 10^{\frac{n}{2}}+z_{1}\cdot 10^{\frac{n}{2}}+z_{0}$
	- ###### Recurrence
		- $T(n)=3T(\frac{n}{2})+O(n)$
		- By solving this we get $T(n)=\Theta(n^{\log_{2}3})=O(n^{1.58})$
		- This is asymptotically faster than the $O(n^2)$ method

- ### Matrix Multiplication
	- Divide and conquer also works on matrices
	- # DO LATER

- ### Recursive Tree Method
	- # DRAW WITH EXCALIDRAW
	- Visualize the work done at each level with a recursion tree

- ### Master Theorem
	- Let $a \ge 1$ and $b > 1$ be constants. Let $f(n)$ be a function, and let $T(n)$ be defined on the non-negative integers by the recurrence $T(n)=aT(\frac{n}{b})+f(n)$
		- If $f(n)=O(n^{\log_{b} a - \epsilon})$ for some constant $\epsilon > 0$ then $T(n)=\Theta(n^{\log_{b} a})$
		- If $f(n)= \Theta(n^{\log_{b} a})$ then $T(n)=\Theta(n^{\log_{b} a} \log n)$
		- If $f(n)=\Omega(Theta(n^{\log_{b} a + \epsilon}))$ for some constant $\epsilon > 0$ and if $af\left(\frac{n}{b}\right)\le cf(n)$ for some constant $c < 1$ and all sufficiently large $n$, then $T(n)=\Theta(f(n))$
	- Each corresponds to the following:
		- The weight increases geometrically from node to leaves
		- The weight is roughly equal in each layer
		- The weight decreases geometrically from node to leaves

- ### Change of Variables
	- Solve the recurrence $T(n)=2T(\sqrt{n}+\log n)$
	- Use substitution: Let $n=2^m$
	- Now the recurrence becomes $S(m)=2S(\frac{m}{2})+m$
	- This is now a standard recurrence
	- $S(m)=O(m \log m) \Rightarrow T(n) = O(\log n \log \log n)$

- ### Unbalanced Trees
	- Upper bounds can be found by bounding the contributions till the larger height
	- Lower bounds can be found by using the smaller height
	- These bounds are not typically tight, look at Akra-Bazzi method
	- # Excalidraw this too

- ### Domain Transformations
	- The actual recurrence have floor and ceiling functions
		- $T(n)=T\left(\lceil \frac{n}{2} \rceil\right)+T\left(\lfloor \frac{n}{2} \rfloor\right) + O(n)$
	- We can ignore them and consider:
		- $T(n)=2T\left(\frac{n}{2}\right)+ O(n)$
		- $T(n)\le 2T\left(\lceil \frac{n}{2} \rceil\right) + n \le 2T(\frac{n}{2}+1)+ n$
		- $S(n)=T(n+2)\Rightarrow S(n)\le2T(\frac{n}{2}+\frac{2}{2}+1)+n+2=2S(\frac{n}{2})+n+2$

- 