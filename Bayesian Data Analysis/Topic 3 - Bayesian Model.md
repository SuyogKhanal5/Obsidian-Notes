
- ### Bayes' Rule to Bayesian Statistics
	- If we think of parameters as being random variables rather than fixed constants, we can use Bayes' Rule with parameters
	- Suppose that we know a distribution for the unknown parameters which we call the prior distribution (or prior) Pr (parameters)
	- Suppose that we have a statistical model for our data, so that we can calculate Pr (data | parameters). This is called the likelihood
	- If we also can calculate the probability of the data without reference to the parameters – Pr (data)
		- This is the normalizing constant, can be called 
			- The model evidence 
			- The marginal likelihood
			- The probability of data 
			- The prior predictive probability of data
	- ###### Posterior Calculation
		- $\text{Pr}(\text{parameters} | \text{data})$ $=\frac{\text{Pr}(\text{data} | \text{parameters})\text{Pr}(\text{parameters})}{\text{Pr}(\text{data})}$
		- $\text{posterior}=\frac{\text{likelihood}\cdot\text{prior}}{\text{normalizing constant}}$

- ### Discrete and Continuous Parameters
	-  $\theta$: the parameter we are interested in  
	- $D$: the data  $$
	P(\theta \mid D) = \frac{P(D \mid \theta) P(\theta)}{P(D)}
	$$
	- If $\theta$ is a discrete parameter:$$
	P(\theta \mid D) = \frac{P(D \mid \theta) P(\theta)}{\sum_{\text{all possible } \theta^*} P(D \mid \theta^*) P(\theta^*)}
	$$
	- If $\theta$ is a continuous parameter:$$
P(\theta \mid D) = \frac{P(D \mid \theta) P(\theta)}{\int P(D \mid \theta^*) P(\theta^*) \, d\theta^*}
$$

- ### Mathematical Model
	- If $\pi$ represents the chances of a success, the following formula can estimate the likelihood of $y$ successes
	- When $\pi$ is known, the distribution is binomial
	- $y|\pi \sim B(6,\pi)$
	- PMF: $f(y|\pi)=$ $6 \choose y$$\pi^y(1-\pi)^{6-y}$

