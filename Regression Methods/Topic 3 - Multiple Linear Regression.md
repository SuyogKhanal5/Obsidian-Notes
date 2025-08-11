
- ### Alert 1: p vs p-1
	- Farways book assumes there are $p-1$ predictors in MLR, and its design matrix is $X$ of size $n\times p$
	- More widely used is $p$ predictors, with $X$ of size $n\times (p+1)$
	- To avoid confusion, if using formula from the book, make $p=p+1$

- ### Least Squares: Best Hyperplane
	- Given any choice in coefficients $(b_{0},b_{1},\dots b_{p})$
		- $\{(x_{1},x_{2},\dots x_{p},y)\in\mathbb{R}^{p+1}:y=b_{0}+b_{1}x_{1}+b_{2}x_{2}+\dots+b_{p}x_{p}\}$
	- When doing simple linear regression, we only have one predictor, so our result is in $\mathbb{R}^{p+1}=\mathbb{R}^2$, making a regression line
	- In Multiple linear regression, we will have more predictors, for example if $p=2$ we will have a hyperplane in $\mathbb{R}^3$
	- Find the $(b_{0},b_{1},\dots b_{p})$ that minimizes $\sum_{i=1}^{n}[y_i-(b_{0}+b_{1}x_{1}+b_{2}x_{2}+\dots+b_{p}x_{p})]^2$
	- Denote the minimizer by $(\hat \beta_{0}, \hat \beta_{1}, \dots \hat \beta_{p})$
	- The best hyperplane minimizes the sum of the squares of the vertical distances from the points to the hyperplane, and is called the **Regression Hyperplane** or **Regression Surface**
	- The estimated regression surface has the form:
		- $\hat Y = \hat \beta_{0}+\hat \beta_{1}X_{1}+\hat \beta_{2}X_{2}+\dots+\hat \beta_{p}X_{p}$

- ### Vector Representation
	- Suppose there are one response $Y$ and 3 predictors $(X_{1},X_{2},X_{3})$ and we get data on $n$ units
	- Data might be presented in tabular form:
		- $\begin{pmatrix} y_{1} & x_{11} & x_{12} & x_{13} \\ y_{2} & x_{21} & x_{22} & x_{23} \\ \vdots & \vdots & \vdots & \vdots \\ y_{n} & x_{n1} & x_{n2} & x_{n3}\end{pmatrix}$
	- Define the vectors:
		- $\vec y=\begin{bmatrix}y_{1}\\y_{2}\\\vdots \\ y_{n}\end{bmatrix}$, $\vec \epsilon=\begin{bmatrix}\epsilon_{1}\\\epsilon_{2}\\\vdots \\ \epsilon_{n}\end{bmatrix}$, and $\vec \beta=\begin{bmatrix}\beta_{0}\\\beta_{1}\\\beta_2 \\ \beta_{3}\end{bmatrix}$
	- Note that $\vec y \in \mathbb{R}^{n}$, $\vec \epsilon \in \mathbb{R}^{n}$, and $\beta \in \mathbb{R}^4$
	- Define the matrix $X \in \mathbb{R}^{n\times4}$
		- $X=\begin{pmatrix} 1 & x_{11} & x_{12} & x_{13} \\ 1 & x_{21} & x_{22} & x_{23} \\ \vdots & \vdots & \vdots & \vdots \\ 1 & x_{n1} & x_{n2} & x_{n3}\end{pmatrix}$
	- The MLR model takes the form:
		- $y_{i}=\beta_{0}+\beta_{1}x_{i1}+\beta_{2}x_{i2}+\beta_{3}x_{i3}+\epsilon_{i}$, $1\le i \le n$
	- It can equivalently be represented in the vector form:
		- $\vec{y}=X\vec \beta +\vec \epsilon$

- ### Vector Representation of MLR
	- MLR model takes the form:
		- $y_{i}=\beta_{0}+\beta_{1}x_{i1}+\beta_{2}x_{i2}+\dots+\beta_{p}x_{ip}+\epsilon_{i}$
	- Define the matrix $X\in\mathbb{R}^{n\times(p+1)}$ called the design/model matrix
		- $X=\begin{pmatrix} 1 & x_{11} & x_{12} & \dots & x_{1p} \\ 1 & x_{21} & x_{22} & \dots & x_{2p} \\ \vdots & \vdots & \vdots & \vdots & \vdots \\ 1 & x_{n1} & x_{n2} & \dots & x_{np} \end{pmatrix}$
	- Define the vectors
		-  $\vec y=\begin{bmatrix}y_{1}\\y_{2}\\\vdots \\ y_{n}\end{bmatrix}$, $\vec \epsilon=\begin{bmatrix}\epsilon_{1}\\\epsilon_{2}\\\vdots \\ \epsilon_{n}\end{bmatrix}$, and $\vec \beta=\begin{bmatrix}\beta_{0}\\\beta_{1}\\\vdots \\ \beta_{p}\end{bmatrix}$
	- Note that $\vec y \in \mathbb{R}^{n}$, $\vec \epsilon \in \mathbb{R}^{n}$, and $\beta \in \mathbb{R}^{p+1}$
	- It can equivalently be represented in the vector form:
		- $\vec{y}=X\vec \beta +\vec \epsilon$

- ### Vector Representation of the i-th unit
	- If $\vec{a},\vec{b}\in\mathbb{R}^m$, then the inner product of $a$ and $b$ is defined as: 
		- $<\vec a,\vec b>$ $=$ $<\vec b,\vec a>$ $=$ $\vec a' \vec b$ = $\vec a \vec b'  = a_1b_1+a_2b_2+\dots+a_mb_m$
	- The $i$-th unit is generated as:
		- $y_{i}=\beta_{0}+\beta_{1}x_{i1}+\beta_{2}x_{i2}+\dots+\beta_{p}x_{ip}+\epsilon_i$
	- Let $x_{i}=(1,x_{i1},x_{i2},\dots,x_{ip})'\in \mathbb{R}^{p+1}$, we can equivalently write $y_{i}=\vec x_{i}' \beta + \epsilon_{i}$

- ### Least Squares: Interpretation I
	- MLR model takes the form $y_i = \beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \cdots + \beta_p x_{ip} + \varepsilon_i, \quad i = 1, \dots, n$
	- Find the $(b_0, b_1, \dots, b_p)'$ that minimizes $\sum_{i=1}^{n} \left[y_i - \left(b_0 + b_1 x_{i1} + b_2 x_{i2} + \cdots + b_p x_{ip}\right)\right]^2$
	- Interpretation I: The "best hyperplane" minimizes the sum of the squares of the vertical distances from the points to the hyperplane, and is called the **Regression Hyperplane** or **Regression Surface**

- ### Vector Representation of the Sum of Squares
	- Let $\mathbf{x}_j$ be the $n$-dimensional vector consisting of the values of the $j$-th predictor $X_j$ observed on the $n$ units, i.e.,  $\mathbf{x}_j = (x_{1j}, x_{2j}, \dots, x_{nj})'$
	- Please pay attention to the difference  between $\mathbf{x}_i$ and $\mathbf{x}_{.j}$
	  - $\mathbf{x}_i = (1, x_{i1}, x_{i2}, \dots, x_{ip})'$ contains all the predictors on the $i$-th unit.
	- Let us consider an example with 3 predictors.
	-   $\begin{pmatrix} y_1 - (b_0 + b_1 x_{11} + b_2 x_{12} + b_3 x_{13}) \\ y_2 - (b_0 + b_1 x_{21} + b_2 x_{22} + b_3 x_{23}) \\ \vdots \\ y_n - (b_0 + b_1 x_{n1} + b_2 x_{n2} + b_3 x_{n3}) \end{pmatrix} = \begin{pmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{pmatrix} - \left[b_0 \begin{pmatrix} 1 \\ 1 \\ \vdots \\ 1 \end{pmatrix} + b_1 \begin{pmatrix} x_{11} \\ x_{21} \\ \vdots \\ x_{n1} \end{pmatrix} + b_2 \begin{pmatrix} x_{12} \\ x_{22} \\ \vdots \\ x_{n2} \end{pmatrix} + b_3 \begin{pmatrix} x_{13} \\ x_{23} \\ \vdots \\ x_{n3} \end{pmatrix}\right]$
	- This simplifies to: 
		- $\mathbf{y} - (b_0 \mathbf{1}_n + b_1 \mathbf{x}_{.1} + b_2 \mathbf{x}_{.2} + b_3 \mathbf{x}_{.3})$
	- Or more compactly:  
		- $\mathbf{y} - \mathbf{Xb}.$
	- Finally due to euclidean norm of $a$:  
		- $\sum_{i=1}^{n} \left[ y_i - (b_0 + b_1 x_{i1} + b_2 x_{i2} + b_3 x_{i3}) \right]^2 = ||\vec{y}-X\vec{b}||^2$

- ### Least Squares: Interpretation II
	- In general for any $\vec b =(b_0, b_1, \dots, b_p)'$ the above formula is true
	- Interpretation II: Find the best linear combinations of the columns of the design matrix such that the euclidean norm is minimized $(||\vec{y}-X\vec{b}||^2$)

- ### Least Squares: Interpretation III:
	- Suppose there is no intercept $\beta_{0}$ and there are two predictors $X_{1}$ and $X_{2}$
	- In this case, $X$ is $n \times 2$
	- The two $n$-dimensional

- $\beta$s must be linear in MLR for it to be LR model