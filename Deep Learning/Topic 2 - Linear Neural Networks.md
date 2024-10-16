
- ### Linear Regression
	- ###### Linear Model
		- One layer Neural Network
		- Consists of learnable weight $\vec{w}$ and input features $\vec{x}$
		- General form: $\hat{y}=w_{1}x_{1}+w_{2}x_{2}+\dots+w_{d}x_{d}+b$
		- Vector form: $\hat{y}=\vec{w}^T\vec{x}+b$
		- Matrix form: $\hat{y}=X\vec{w}+b$
	- ###### Neural Network Interpretation
		- Weights can be considered as the connection between neurons

- ### Loss Function
	- How to measure the quality of the model
	- Squared loss (L2 loss) for one pair $(x,y)$
		- $l^{(i)}(\vec{w},b)=\frac{1}{2}(\hat{y}^{(i)}-y^{(i)})^2$
	- Mean Squared Error for whole dataset
		- $L(\vec{w},b)=\frac{1}{n}\sum_{i=1}^{n}l^{(i)}(\vec{w},b)=\frac{1}{n}\sum_{i=1}^{n}\frac{1}{2}(\vec{w}^T\vec{x}^{(i)}+b-y^{(i)})^2$

- ### Learning Algorithm
	- How to fit the model: minimize the total loss across all training samples
		- $\vec{w}*, b*=\text{argmin } L(\vec{w},b)$
	- We can solve this analytically (closed form) or iteratively
	- ###### Analytical Solution
		- For linear models we can find the global optimum analytically
		- The objective can be written as $||\vec{y}-X\vec{w}||^2_2$
			- Which is a quadratic form and convex (no local minima) with respect to $\vec{w}$
		- Taking derivative of the objective with respect to $\vec{w}$ and setting it to $0$ yields the analytical solution $\vec{w}^*=(X^TX)^{-1}X^Ty$

- ### Iterative Learning With Gradient Descent
	- Most effective models like deep neural networks are non linear models for which an analytical solution is not available
	- We can still learn the model if the loss function is continuous with respect to the parameter $\vec{w}$ by the gradient descent method
	- Compute the gradient by $\frac{dL}{d\vec{w}}$ and update the parameter as follows:
		- $\vec{w} \leftarrow \vec{w}-\eta \frac{\partial L}{\partial \vec{w}}$
		- $\eta$ is learning rate/step size. It is also the hyperparameter. We need to do hyperparameter tuning to search for the right model
	- Like rolling a ball on the surface of the loss function
	- In non convex problems we can only find one local minimum![[Pasted image 20240919161337.png]]
	
- ### Stochastic Gradient Descent
	- Because the true gradient is a sum of all sample-wise gradient, computing the full gradient can be expensive if the dataset is large
	- We can use a mini batch randomly sampled from the full gradient to estimate the gradient
	- Importantly, this is unbiased with uniform sampling, meaning we still get the same solution in expectation
	- Final update rule
		- $\vec{w}\leftarrow \vec{w}-\frac{\eta}{|\mathcal{B}|}\sum_{i\in \mathcal{B}} \partial_{\vec{w}}l^{(i)}(\vec{w},b)=w-\frac{\eta}{|\mathcal{B}|}\sum_{i\in \mathcal{B}}\vec{x}^{(i)}(\vec{w}^T\vec{x}^{(i)}+b-y^{(i)})$
		- $b\leftarrow b-\frac{\eta}{|\mathcal{B}|}\sum_{i\in \mathcal{B}} \partial_{b}l^{(i)}(\vec{w},b)=b-\frac{\eta}{|\mathcal{B}|}\sum_{i\in \mathcal{B}}\vec{x}^{(i)}(\vec{w}^T\vec{x}^{(i)}+b-y^{(i)})$
	- This can reach different solutions due to different batch selection

- ### Probabilistic vs. Deterministic Learning
	- Modeling uncertainty of the prediction is important
	- Because the impact (loss) of each decision can be very different
		- Predict {stockPriceUp, stockPriceDown}
			- If stockPriceDown, should we sell
		- What if stockPriceDown has 51% certainty and stockPriceUp has 49%?
	- We want $p(y|x)$ instead of $y=f(x)$

- ### Probabilistic Linear Regression Model
	- We can use a Gaussian distribution to probabilistically model the linear regression problem 
		- $p(x)=\frac{1}{\sqrt{2\pi\sigma^2}}\text{exp}(-\frac{1}{2\sigma^2}(z-\mu)^2)$
	- By setting $\mu=\vec{w}^T\vec{x}+b$ and $\sigma$ as hyperparameter
	- Model: We have Gaussian linear regression model
		- $P(y|x)=\frac{1}{\sqrt{2\pi\sigma^2}}\text{exp}(-\frac{1}{2\sigma^2}(y-\vec{w}^T\vec{x}-b)^2)$
	- Equivalently: $y=\vec{w}^T\vec{x}+b+\epsilon$ where $e~\aleph(0,\sigma^2)$
	- ###### Loss Function
		- Larger likelihood $p(y^{(i)}|x^{(i)}) \rightarrow$ fits better $\rightarrow$ better $\vec{w}$ and $b$
		- According to maximum likelihood principle the best parameters are those that maximize the likelihood of the whole dataset
			- $p(\vec{y}|X)=\prod_{i = 1}^{n} p(y^{(i)}|x^{(i)})$
		- Estimators chosen according to this principle are called maximum likelihood estimators (MLE)
	- ###### Negative Log Likelihood
		- Maximizing the product of many exponential functions becomes simple by taking log (and negative sign to make as a minimization problem)
		- This gives the **Negative Log Likelihood** an objective of
			- $-\log P(\vec{y}|X)=\sum_{i=1}^{n}\frac{1}{2}\log(2\pi\sigma^2)+\frac{1}{2\sigma^2}(y^{(i)}-\vec{w}^T\vec{x}^{(i)}-b)^2$
		- Notice how the objective is similar and different from non probabilistic linear regression
		- Thus, minimizing squared error is equivalent to MLE of a linear model under assumption of additive Gauss noise
		- Instead of using the same $\sigma$ for all data points, we can use another network to predict $\sigma^{(i)} \text{ } \forall \text{ } \vec{x}^{(i)}$
			- $\mu^{(i)}=\vec{w}^T_{\mu}\vec{x}^{(i)}+b_{\mu}$
			- $\sigma^{(i)}=\vec{w}^{T}_{\sigma}\vec{x}^{(i)}+b_{\sigma}$

- ### Linear Classification with Softmax
	- In regression, the label $(y)$ is a real value
	- In classification we represent the class label as a one hot vector
	- Ex. $[1,0,0]$ is cat, $[0,1,0]$ is dog, $[0,0,1]$ is chicken ![[Pasted image 20240924160607.png]]