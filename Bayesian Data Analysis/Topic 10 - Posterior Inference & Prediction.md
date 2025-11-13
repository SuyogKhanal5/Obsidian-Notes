
- ### Three common types of tasks
	- ###### Posterior estimation
		- Central tendencies: mean, mode, median
		- Variability: variance, quantile
		- Credible intervals
	- ###### Posterior hypothesis testing
		- Posterior tail probabilities
		- Posterior odds and Bayes factor
	- ###### Posterior prediction

- ### Credible Interval
	- Counterpart of confidence interval
	- Incorporate both location and spread of the posterior
	- Interpretation: there is a $\alpha$% **posterior** probability that the parameter is inside this interval. E.g. a 90% credible interval for $\pi$
		- $P(\pi \in (\underline{\pi}, \overline{\pi})) = \int_{\underline{\pi}}^{\overline{\pi}} f(\pi|y)d\pi = 90\%$
	- Two main approaches to constructing a credible interval
		- Central posterior credible interval
		- Highest (posterior) density credible interval
		- The difference between the two approaches is small when the distribution is close to symmetric

- ### Posterior Hypothesis Testing
	- An article claims that fewer than 20% of museum artists are Gen X or younger
		- Frequentist approach: one sample proportion test
		- $H_0: \pi = 0.2$, $H_a: \pi < 0.2$ (or equivalently $H_0: \pi \geq 0.2$, $H_a: \pi < 0.2$)
	- How plausible is this statement in light of our posterior model for $\pi$?
		- $P(\pi < 0.2|y = 14) = ?$
		- `pbeta(0.20, 18, 92)'
		- `## [1] 0.8489856`
	- A portion of the posterior probability of $H_a$ is due to the prior probability of $H_a$, which was set by us. How to draw a fair comparison?![[Pasted image 20251109125300.png]]

- ### Bayes Factor
	- ###### Bayes Factor (BF)
		- $BF = \frac{P(y|H_a)}{P(y|H_0)} = \frac{P(H_a|y)/P(H_0|y)}{P(H_a)/P(H_0)}$
		- Is it more likely to observe the data under $H_a$ or is more likely to observe the data under $H_0$?
		- Provide insight into just how much our understanding about the hypotheses evolved upon observing the data, by comparing the posterior against the prior
		- For one sided test, $P(H_0|y) = 1 - P(H_a|y)$, $P(H_0) = 1 - P(H_a)$
			- BF = posterior odds / prior odds
	- ###### Compare Bayes factor to 1
		- BF = 1: The plausibility of $H_a$ didn't change given the observed data
		- BF > 1: The plausibility of $H_a$ increased given the observed data
		- BF < 1: The plausibility of $H_a$ decreased given the observed data
		- The greater the BF, the **more convincing** evidence for $H_a$

- ### Bayesian Hypothesis Testing
	- ###### Bayesian hypothesis testing vs frequentist hypothesis testing
		- No need for significance level because the testing is based on posterior probabilities
		- Allow for a more flexible interpretation
		- Generally, we don't use the term "reject the null" or "fail to reject", but instead quantify **degrees of belief** or **levels of evidence** for competing hypotheses
			- Bayesian inference doesn't treat hypotheses as fixed, testable truth
	- ###### Relationship between credible interval and testing
		- A credible interval does not directly correspond to hypothesis testing in the same way that a confidence interval does in frequentist approach

- ### What if a Two-Sided Test?
	- If we have $H_0: \pi = 0.3$, $H_a: \pi \neq 0.3$
		- $P(H_0|y) = 0$, $P(H_0) = 0$, BF not meaningful
	- ###### Intuition:
		- The credible interval we got is (0.0853, 0.2647)
		- 0.3 falls "**substantially**" outside of the posterior interval, so in favor of $H_a$
		- How to define "substantially"
	- ###### Method: Create a "range of indifference" around the point null – fatten it up
		- It is best practice to define this range **ahead of time** – before seeing any data. The Bayes factor depends on this range
			- Definition of "substantially"
		- e.g. $H_0: \pi \in (0.25, 0.35)$, $H_a: \pi \notin (0.25, 0.35)$

- ### Posterior Prediction
	- Suppose MoMA will display 20 more artworks. How many among them would you predict are done by Gen X artists or younger?
	- ###### Two sources of uncertainty in posterior prediction:
		- Posterior variability in $\pi$. This is described by the posterior $f(\pi|y = 14) \sim Beta(18, 92)$
		- Sampling variability in $\tilde{y}$. This is described by the sampling model of the new data $f(\tilde{y}|\pi) \sim Bin(20, \pi)$
	- ###### Weigh new data likelihood by the posterior probability distribution:
		- $f(\tilde{y}|\pi)f(\pi|y = 14)$
		- This captures the chance of observing a particular $\tilde{y}$ given $\pi$ while accounting for the posterior uncertainty about $\pi$
		- The calculated probability depends on $\pi$
	- $f(\tilde{y}|\pi)f(\pi|y)$ at different $\pi$![[Pasted image 20251109151523.png]]
	- ###### Posterior predictive model
		- Predict a new observation $\tilde{y}$ given that we have $y$
		- The overall chance of observing the new $\tilde{y}$ across all possible $\pi$ values
		- $f(\tilde{y}|y) = \int f(\tilde{y}|\pi)f(\pi|y)d\pi$
			- We average the possible predictions $f(\tilde{y}|\pi)$ over all possible value of $\pi$, weighting each by how likely that $\pi$ is given our data

- ### Beta-Binomial Distribution
	- Prior: $\pi \sim Beta(\alpha, \beta)$
	- Data: $y|\pi \sim Bin(n, \pi)$
	- Posterior: $\pi|y \sim Beta(\alpha_y, \beta_y)$ $(\alpha_y = \alpha + y, \beta_y = \beta + n - y)$
	- New data: $\tilde{y}|\pi \sim Bin(m, \pi)$
	- $f(\tilde{y}|y) = \int f(\tilde{y}|\pi)f(\pi|y)d\pi$
	  $$= \int \binom{m}{\tilde{y}} \pi^{\tilde{y}}(1-\pi)^{m-\tilde{y}} \frac{1}{B(\alpha_y, \beta_y)} \pi^{\alpha_y - 1}(1-\pi)^{\beta_y - 1} d\pi$$
	  $$= \text{ ... (typical trick)}$$
	  $$= \binom{m}{\tilde{y}} \frac{B(\tilde{y} + \alpha_y, m - \tilde{y} + \beta_y)}{B(\alpha_y, \beta_y)}$$
		- This is called Beta – Binomial distribution: $BetaBin(m, \alpha_y, \beta_y)$
	- ###### Beta – Binomial distribution
		- Mean: $\mu = \frac{m\alpha_y}{\alpha_y + \beta_y}$
		- Variance: $\sigma^2 = \frac{m\alpha_y\beta_y(\alpha_y + \beta_y + m)}{(\alpha_y + \beta_y)^2(\alpha_y + \beta_y + 1)}$

- ### Other Predictive Models
	- ###### Gamma – Poisson
		- Prior: $\lambda \sim Gamma(s, r)$
		- data: $y|\lambda \sim Poisson(\lambda)$
		- Posterior: $\lambda|y \sim Gamma(s_y, r_y)$ $(s_y = s + n\bar{y}, r_y = r + n)$
		- New data: $\tilde{y}|\lambda \sim Poisson(\lambda)$
		- Posterior predictive: $\tilde{y}|y \sim NegativeBinomial(s_y, \frac{1}{1+r_y})$
	- ###### Normal – Normal
		- Prior: $\mu \sim N(\theta, \tau^2)$
		- data: $y|\mu \sim N(\mu, \sigma^2)$
		- Posterior: $\mu|y \sim N(\theta_n, \tau_n^2)$
		- New data: $\tilde{y}|\mu \sim N(\mu, \sigma^2)$
		- Posterior predictive: $\tilde{y}|y \sim N(\theta_n, \tau_n^2 + \sigma^2)$

- ### Posterior Analysis
	- ###### What if the posterior doesn't have a closed form solution?
		- Grid approximation
		- MCMC `stan()` method
		- MCMC M-H method
	- ###### Use Markov chain sample values
		- MoMA artist example
		- Should still perform visual and numerical diagnostics
		- MCMC using `stan()` output
		- Show output using Metropolis-Hastings


