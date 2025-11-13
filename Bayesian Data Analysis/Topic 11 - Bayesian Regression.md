
- ### Bayesian Linear Regression
	- We see the likelihood
	- We need prior assumptions
	- ###### Prior for $\beta_0, \beta_1, \sigma$
		- We assume they are **independent**
			- We assume our prior understanding of where the model "lives" $(\beta_0)$, the ridership change in relation to temperature $(\beta_1)$, and strength of relationship $(\sigma)$, are all unrelated with one another
			- It is entirely possible that the **posterior** distributions of these parameters become **dependent** – if it happens, we would have learned that from the model and the data
		- $\beta_0 \sim N(m_0, s_0^2), \beta_1 \sim N(m_1, s_1^2)$
			- $m_0, s_0^2, m_1, s_1^2$ are the hyperparameters chosen to match our prior understanding about $\beta_0$ and $\beta_1$
		- $\sigma \sim Exp(l), E(\sigma) = 1/l, V(\sigma) = 1/l^2$
			- Restricted to positive values, and weakly informative
			- This is the default prior in `rstanarm` package. Alternatives include half-Cauchy and inverse Gamma distributions

- ### Bayesian Linear Model
	- ###### Prior:
		- $\beta_0 \sim N(m_0, s_0^2), \beta_1 \sim N(m_1, s_1^2), \sigma \sim Exp(l)$
		- They are independent
	- ###### Data: $y_i | \beta_0, \beta_1, \sigma \sim N(\mu_i, \sigma^2)$, where $\mu_i = \beta_0 + \beta_1 x_i$
	- ###### We want to find the posterior distribution
		- Joint distribution $f(\beta_0, \beta_1, \sigma|y_i) = ?$
			- The posterior distribution involves a product of a normal likelihood with normal and exponential priors.
			- The conjugacy properties do not work, no closed form solution
		- Marginal distributions:
			- $f(\beta_0|y_i) = ? f(\beta_1|y_i) = ? f(\sigma|y_i) = ?$
			- Marginal posterior for each parameter also has no closed form solution
	- We use MCMC to approximate the distributions

- ### Choosing Prior Parameters
	- Suppose we have the following prior understanding
		- On an **average** temperature day (65-70F), there are typically around 5000 rides, and could be somewhere between 3000 and 7000
			- $\beta_{0c} = \beta_0 + \beta_1 \bar{x}$
			- It is the centered intercept
		- For every one degree increase in temperature, ridership typically increases by 100 rides, and could be as low as 20 or as high as 180
		- At any given temperature, daily ridership will tend to vary with a moderate SD of 1250 rides
			- $E(\sigma) = 1/l = 1250$, $l = 0.0008$
	- ###### Method 2 prior :
		- $\beta_{0c} \sim N(5000, 1000^2), \beta_1 \sim N(100, 40^2), \sigma \sim Exp(0.0008)$
	- ###### Method 1 prior: What is the distribution of $\beta_0$?

- ### Structural Relationship
	- Do we have ample posterior evidence that there's a positive association between ridership and temperature?
		- Visual evidence: All realized posterior regression lines clearly show a positive slope
		- Numerical evidence: Based on posterior credible interval: output from `tidy()` shows credible interval well above 0
		- Numerical evidence from posterior probability: calculate $P(\beta_{1}> 0 | y)$ (empirical probability from 20,000 MCMC draws) and see whether it is close to 1

- ### Uncertainty in Sigma
	- The parameter $\sigma$ describes the degree to which ridership varies on days of the same temperature
	- Posterior results and uncertainty for ᵰ can be visualized via repeated simulation of ridership data under various posterior plausible values of $\sigma$
