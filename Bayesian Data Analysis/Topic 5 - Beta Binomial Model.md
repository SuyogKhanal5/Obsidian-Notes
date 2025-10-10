
- ### Beta Binomial Model
	- Prior Distribution: $\pi \sim \text{Beta}(\alpha,\beta)$
		- $f(\pi)=\frac{1}{B(\alpha,\beta)}\pi^{\alpha-1}(1-\pi)^{\beta-1}$
	- For a given $\pi$, the data model is $y|\pi \sim B(n,\pi)$
		- $f(y|\pi)= {n \choose y}\pi^{y}(1-\pi)^{n-y}$ (where $y=0,1,\dots n$)
		- Likelihood: $L(\pi|y)={n \choose y}\pi^{y}(1-\pi)^{n-y}$
	- ###### Posterior
		- Formula
			- $f(y|\pi)=\frac{\text{likelihood}\cdot \text{prior}}{\text{normalizing constant}}$
			- $f(y|\pi)\propto L(\pi|y)f(\pi)$
			- $f(y|\pi)\propto {n \choose y}\pi^{y}(1-\pi)^{n-y}\frac{1}{B(\alpha,\beta)}\pi^{\alpha-1}(1-\pi)^{\beta-1}$
			- $f(y|\pi)\propto \pi^{a+y-1}(1-\pi)^{\beta+n-y-1}$
		- ***Distribution***
			- We can ignore the constant terms because they do not depend on the parameters we are estimating
				- The binomial coefficient only depends on $n$ and $x$, not on $\alpha,\beta$
			- **Fact 1**: It is a function proportional to $\pi^{a+y-1}(1-\pi)^{\beta+n-y-1}$
				- Called the kernel of the density
					- Any factors that are not functions of any variables in the domain are omitted
				- The kernel is the same as the kernel in the beta distribution
			- **Fact 2**: It is a probability distribution (integrate to 1)
				- Once the kernel is examined and matched to a known distribution, the normalization factor can be reinstated
			- It must have a normalizing constant $\frac{1}{B(\alpha+y,\beta+n-y)}$
		- The posterior distribution is also a beta distribution with parameters $\alpha+y, \beta+n-y$, the density function is as follows:
			- $f(x)=\frac{1}{B(\alpha+y,\beta+n-y)}x^{\alpha+y-1}(1-x)^{\beta+n-y-1}$
				- Literally just the Beta distribution's PDF function but with $\alpha+y$ substituted in for $\alpha$ and $\beta+n-y$ substituted in for $\beta$
		- ***Properties***
			- Mean: $E(\pi|y)=\frac{\alpha+y}{\alpha+y+b+n-y}=\frac{\alpha+y}{\alpha+b+n}$
				- Same deal as the PDF, its the same as the Beta distribution's mean formula, but with $\alpha+y$ substituted in for $\alpha$ and $\beta+n-y$ substituted in for $\beta$
			- **How the prior and data affect the posterior**
				- Prior mean from Beta: $E(\pi)=\frac{\alpha}{\alpha+\beta}$
				- Observed proportion (mean) from data: $\frac{y}{n}$
				- Rewrite the posterior mean
					- $E(\pi|y)=\frac{\alpha+y}{\alpha+b+n}+\frac{y}{\alpha+\beta+n}$
					- $E(\pi|y)=\frac{\alpha+y}{\alpha+b+n}\cdot \frac{\alpha}{\alpha+\beta}+\frac{n}{\alpha+\beta+n}\cdot\frac{y}{n}$
					- $W \cdot \text{prior mean} + (1-W)\cdot \text{data mean}$
				- It is the weighted average of the prior mean and the data mean
			- Variance: $\text{Var}(\pi|y)=\frac{(\alpha+y)(\beta+n-y)}{(\alpha+\beta+n)^2(\alpha+\beta+n+1)}$
				- The expected posterior variance is always smaller than the prior variance
				- $\text{Var}(\theta)=E(\text{Var}(\theta|X))+\text{Var}(E(\theta|X))$
				- When new data is observed the contributed information about the unknown parameter, therefore we expect to reduce the uncertainty about the parameter. 
				- If the prior and likelihood are in stark contrast, only then will the variance increase
			- Mode: $\text{Mode}(\pi|y)=\frac{\alpha+y-1}{\alpha+\beta+n-2}$
			- **How does the data affect the posterior**
				- What happens when there is more and more data
				- As $n \rightarrow \infty$, prior weight $\frac{\alpha+\beta}{\alpha+\beta+n}\rightarrow 0$, data weight $\frac{n}{\alpha+\beta+n}\rightarrow 1$, posterior mean $E(\pi|y)\rightarrow \lim_{n\rightarrow\infty}\frac{y}{n}$
					- Is $\lim_{n\rightarrow\infty}\frac{y}{n}=0$
					- It is the stabilized proportion of success from data
			- The more data we have the more the posterior mean will drift towards trends exhibited in the data as opposed to the prior
				- The rate at which this drift occurs will depend on the prior, whether it is informative or vague
				- The data will speak so long as we're not stubborn, i.e assigning a prior probability of zero to certain parameter values
			- **How does the prior affect the posterior**
				- When $\alpha,\beta$ are sufficiently large compared to $n$
					- $\frac{\alpha+\beta}{\alpha+\beta+n}\approx1,\frac{n}{\alpha+\beta+n}\approx0$, posterior mean $E(\pi|y)\approx\frac{\alpha}{\alpha+\beta}$
				- When $\alpha$ is sufficiently large compared to $n$
					- $\frac{\alpha+\beta}{\alpha+\beta+n}\approx1,\frac{n}{\alpha+\beta+n}\approx0$, posterior mean $E(\pi|y)\approx\frac{\alpha}{\alpha+\beta}\approx 1$
				- When $\beta$ is sufficiently large compared to $n$
					- $\frac{\alpha+\beta}{\alpha+\beta+n}\approx1,\frac{n}{\alpha+\beta+n}\approx0$, posterior mean $E(\pi|y)\approx\frac{\alpha}{\alpha+\beta}\approx 0$
				- When $\alpha,\beta$ are sufficiently small compared to $n$
					- $\frac{\alpha+\beta}{\alpha+\beta+n}\approx0,\frac{n}{\alpha+\beta+n}\approx1$, posterior mean $E(\pi|y)\approx\frac{y}{n}$

- ### Beta Binomial Summary$$
\begin{array}{|c|c|c|}
\hline
 & \textbf{Density} & \textbf{Mean} \\
\hline
\text{Prior} & 
f(\pi) = \frac{1}{B(\alpha,\beta)} \pi^{\alpha-1}(1-\pi)^{\beta-1} 
& \frac{\alpha}{\alpha+\beta} \\
\hline
\text{Likelihood} & 
L(\pi|y) = \binom{n}{y} \pi^y (1-\pi)^{n-y} 
& \\
\hline
\text{Posterior} & 
f(\pi|y) = \frac{1}{B(\alpha+y,\;\beta+n-y)} \pi^{\alpha+y-1}(1-\pi)^{\beta+n-y-1} 
& \frac{\alpha+y}{\alpha+\beta+n} \\
\hline
\end{array}
$$
- ### Sequential Bayesian Analysis
	- In a sequential Bayesian analysis, a posterior model is updated incrementally as more data comes in
	- With each new piece of data, the previous posterior model reflecting out understanding before observing this data becomes the new prior model
	- The final posterior model is data order invariant, i.e it isn't impacted by the order in which we observe the data
	- The posterior distribution obtained after updating the data step by step is the same as the posterior obtained by using all of the data at once
	- The final posterior only depends on the cumulative data
		- When you update the posterior in a stepwise manner, you are essentially multiplying the likelihoods of the new data points with the current prior at each step, which is the same as multiplying the combined likelihood (from all the data) with the prior

- ### Conjugate
	- **Conjugate Prior**: We say that $f(\pi)$ is a conjugate prior for the likelihood $L(\pi|y)$ if the posterior $f(\pi|y)$ is from the same model family as the prior
	- **Conjugate Families**: The combination of the class of conjugate priors and their corresponding class of data likelihoods
		- Beta-Binomial is a conjugate family
	- ###### Why Conjugate Priors
		- A prior should reflect our state of knowledge about the parameter of interest, before seeing the data
		- There are other, more practical criteria to consider when choosing a prior
			- **Computational ease**: Especially if we don't have access to computing power, it is helpful if the posterior model is easy to build
			- **Interpretability**: We've seen that posterior models are a compromise between the data and the prior model. A posterior model is interpretable, and thus more useful, when you can look at its formulation and identify the contribution of the data relative to that of the prior