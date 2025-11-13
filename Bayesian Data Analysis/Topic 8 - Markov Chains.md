
- ### Markov Chain
	- ###### A stochastic process for a sequence of events
		- The probability of each event depends only on the state attained in the previous event
			- Conditional on the present state of the system, future and past states are independent
			- Sometimes called "memoryless"
		- Discrete-Time MC (DTMC), Continuous-Time MC (CTMC)
	- ###### Examples
		- Random walk (drunkard's walk)
		- Independent trials
		- Real life examples
			- Board games played with dice
			- Weather prediction model

- ### Stationary Distribution
	- Also called equilibrium distribution
	- It is the stable, long-term set of probabilities for each state, and doesn't depend on the starting point
		- Suppose you are moving between different "states" over time
			- The probabilities from one state to another might depend on the state you're currently in, but they remain fixed over time
		- If (after moving many times) the probability of being in any particular state remains the same $\implies$ reaches a balance (you still move but the overall likelihood doesn't change anymore)
			- The system "settles down" (stationary distribution)
	- Not all Markov chains has stationary distribution
		- Random walk on the real number line doesn't

- ### Monte Carlo (MC) Simulation
	- Work by John von Newmann and Stanislaw Ulam
		- Stanislaw Ulam invented modern version of Markov Chain Monte Carlo method (MCMC)
	- Especially useful when closed form solution not available
		- Complexity of the problem or degree of computation
		- The distribution of the statistic of interest is unknown or can't be derived simply
	- ###### How does it work
		- Specify the probability distribution of the outcome
		- Run simulations repeatedly and generate random values of the outcome

- ### Markov Chain Monte Carlo (MCMC)
	- Draw samples from a probability distribution
	- Given a probability distribution, one can construct a Markov chain whose elements' distribution **approximates** it, that is, the Markov chain's equilibrium distribution matches the target distribution
	- Useful for distributions that are too complex or too highly dimensional to study
		- Primarily used for calculating numerical approximations of multi-dimensional integrals
	- Methods include
		- Metropolis-Hastings algorithm
		- Gibbs sampling

- ### MCMC in Bayesian
	- A Markov chain sample of length $N$: $\{\theta^{(1)}, \theta^{(2)}, ..., \theta^{(N)}\}$
		- $\theta^{(2)}$ is drawn from some distribution that depends on $\theta^{(1)}$
		- $\theta^{(3)}$ is drawn from some distribution that depends on $\theta^{(2)}$
		- ...
		- Generally: $\theta^{(i)}$ is drawn from some distribution that depends on $\theta^{(i-1)}$: $q(\theta^{(i)}|\theta^{(i-1)},\vec{y})$
	- What is that "some distribution"?
		- Not the posterior distribution
	    • $q(\theta^{(i)}|\theta^{(i-1)},\vec{y}) \neq f(\theta^{(i)}|\vec{y})$
	- $q$ is designed in a way such that the Markov chain's stationary distribution is the posterior
	    • $\theta^{(i)} \sim f(\theta^{(i)}|\vec{y})$
	- ###### MCMC property:
	  – $q(\theta^{(i)}|\theta^{(i-1)},\theta^{(i-2)},...,\theta^{(1)},\vec{y}) = q(\theta^{(i)}|\theta^{(i-1)},\vec{y})$
	- We are trying to get the posterior, we don't know the posterior
		- How can we design a Markov chain with its stationary distribution equal to the posterior
	- We can calculate the posterior up to a constant
		- $f(\theta|D) = \frac{f(D|\theta)f(\theta)}{\int f(D|\theta^*)f(\theta^*)d\theta^*}$
	- ###### Grid approximation vs. MCMC
		- When generating samples, both are not generating from the posterior
			- Grid approximation generate from the discretized approximation of posterior
		- Grid approximation has independent samples, MCMC has dependent samples

- ### MCMC Diagnostics
	- ###### What we want
		- The Markov chain to mimic a random sample that eventually converges to the target/stationary distribution - our Bayesian posterior
	- ###### Reality
		- MCMC works well for the Beta-Binomial model
			- Does it work for all models?
				- We don't know the posterior, we don't know for certain whether a specific Markov chain has converged
	- ###### Diagnostics
		- What does a good Markov chain look like?
		- How can we tell if our Markov chain sample produces a reasonable approximation of the posterior?
		- How big should our Markov chain sample size be?

- ### Visual Diagnostics
	- ###### Ideal individual trace plot
		- Exhibit no discernible trends, drifts, or notable phenomena
		- Has a stable mean across the iterations
		- Has a stable variance across the iterations
		- Look similar to a bunch of white noise
	- ###### Ideal multiple super-imposed parallel chains trace plot
		- Look similar with no discernible differences among the chains
		- Be stable around the same mean
		- Be stable with the same variance
		- Have density plots or histograms that align closely

- ### Numerical Diagnostics
	- Effective sample size $N_{eff}$
		- The number of **independent** samples it takes to produce an equivalently accurate posterior approximation
		- For the same number of iterations $N$, the larger the $N_{eff}$, the better
		- Typically $N_{eff} \leq N$, or $\frac{N_{eff}}{N} \leq 1$ (called effective sample size ratio)
			- `neff_ratio(bb_sim, pars = c("pi"))`
			- `0.3586` for previous example
		- A ratio of, say, less than 10% should raise suspicion on the Markov chain's quality
	- ###### Autocorrelation
		- Measures the correlation between pairs of values that belong to the same Markov chain
		- Autocorrelation of lag $k$
		- The correlation between pairs of values that are "$k$ steps apart":
		  $\pi^{(1)} \& \pi^{(k+1)}, \pi^{(2)} \& \pi^{(k+2)}, ...$
	- ###### Ideal case: mixing quickly
		- The autocorrelation quickly drops off and is effectively 0 by lag 5
		- Fast-mixing chains exhibit behavior similar to that of an independent sample
	- `grid.arrange(mcmc_trace(bb_sim, pars = "pi")
	- $\hat{R}$ (R-hat) measures the consistency across parallel chains
		- Compare the variability in sampled $\pi$ values across all chains combined, and variability within each individual chain
		- $\hat{R} \approx \sqrt{\frac{Var_{combined}}{Var_{within}}}$
			- $Var_{combined}$: the variability across all chains combined
			- $Var_{within}$: the typical variability within any individual chain
			- `rhat(bb_sim, pars = "pi")`
			- `1.000341` for previous example
		- Ideally, $\hat{R}$ should be very close to 1. $\hat{R} > 1.05$ should raise suspicion regarding the stability of the simulation

- ### Fast, Slow and Thin Mixing
	- ###### Fast mixing chains
		- Exhibit behavior similar to that of an independent sample
		- The chain move quickly around the range of posterior plausible values
		- Autocorrelation drops off quickly
		- Effective sample size ratio is reasonably large
	- ###### Slow mixing chains
		- Basically just the opposite of fast mixing chains
	- Deal with slow mixing chains (even if eventually it produces good posterior approximation)
		- Thin the Markov chain: keep every X chain values $\implies$ remove strong correlation at low lags