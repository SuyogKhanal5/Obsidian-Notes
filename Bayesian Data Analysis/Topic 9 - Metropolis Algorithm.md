
- ### Metropolis-Hastings
	- Target distribution is posterior
		- $f(\theta|D) = \frac{L(\theta|D)f(\theta)}{\text{Normalizing Constant}}$
		- We don't know it, but we know it up to a constant
	- Design the chain: from a current point $\theta$, propose a new point $\theta^*$, in a random way, but depends on $\theta$
	- Define the probability of accepting $\theta^*$ such that
		- The Markov chain has the stationary distribution as posterior – how?
		- The moving from $\theta$ to $\theta^*$ should also be intuitively correct
	- If we accept it, the chain goes to the new point $\theta^*$. Otherwise, the chain stays put at $\theta$ for this iteration
	- Repeats

- ### Some Preparation
	- ###### Reversible Markov chain
		- If the reversed process is the same as the forward process
		- Not all MC are reversible
	- ###### Detailed balance condition
		- Target distribution $g(x)$
		- Any two states $x,x'$
		- Transition probability $P(x\rightarrow x')$
		- $g(x)P(x\rightarrow x')=g(x')P(x'\rightarrow x)$
	- Reversible Markov chain $\iff$ satisfies detailed balance condition (reversible with respect to $g(x)$)
	- Reversible Markov chain $\Rightarrow$ it has a stationary distribution as the target distribution
	- Key in Metropolis or Metropolis-Hastings
		- Create a Markov chain such that is reversible with respect to the posterior, then it has a stationary distribution as the posterior

- ### Metropolis-Hasting Details
	1. Pick an initial point $\theta^{(0)} = \theta$ in the parameter space at random based on some distribution (typically a normal distribution)
	2. Use another distribution, called the proposal distribution to propose a new point $\theta^*$ at random, e.g. $q(\theta^*|\theta) = N(\theta, \sigma^2)$ (symmetric for Metropolis, and asymmetric for Metropolis – Hastings)
	3. Assess the ratio $r = \frac{f(\theta^*)L(\theta^*|D)}{f(\theta)L(\theta|D)} \frac{q(\theta|\theta^*)}{q(\theta^*|\theta)}$ and decide whether to accept or reject the proposal based on $r$: the acceptance probability from $\theta$ to $\theta^*$: $A(\theta \to \theta^*) = \min(1, r)$
	4. If we accept the proposal, the chain moves to $\theta^*$. That is, record $\theta^{(1)} = \theta^*$. If we reject the proposal, the chain stays put at $\theta$. That is, $\theta^{(1)} = \theta$. Note: in this case, $\theta^{(1)}$ repeats its predecessor $\theta^{(0)}$ **The transition probability is the product of proposal and acceptance probability**
	5. Repeat Steps 2 - 4 to obtain a Markov chain of desired length: $\{\theta^{(1)}, \theta^{(2)}, ..., \theta^{(N)}\}$

- ### Why $\gamma$ and $A(\theta \rightarrow \theta*)$ Defined this way?
	- Keep in mind that we want the chain to be reversible with respect to the posterior, so it has a stationary distribution as posterior
		- $f(\theta|D)P(\theta\to\theta^*) = f(\theta^*|D)P(\theta^*\to\theta)$
	- $\frac{f(\theta)L(\theta|D)}{NC} q(\theta^*|\theta)A(\theta\to\theta^*) = \frac{f(\theta^*)L(\theta^*|D)}{NC} q(\theta|\theta^*)A(\theta^*\to\theta)$
		- The normalizing constant is unnecessary (even though we don't know what the posterior is, it doesn't affect us to build the Markov chain)
	- $\frac{A(\theta\to\theta^*)}{A(\theta^*\to\theta)} = \frac{f(\theta^*)L(\theta^*|D)}{f(\theta)L(\theta|D)} \frac{q(\theta|\theta^*)}{q(\theta^*|\theta)} = r$
		- $r$ is the ratio of acceptance probabilities
		- If $r < 1$, $\frac{A(\theta\to\theta^*)}{A(\theta^*\to\theta)} = r$, let's define $A(\theta\to\theta^*) = r$, $A(\theta^*\to\theta) = 1$
		- If $r > 1$, $\frac{A(\theta\to\theta^*)}{A(\theta^*\to\theta)} = r$, let's define $A(\theta\to\theta^*) = 1$, $A(\theta^*\to\theta) = \frac{1}{r}$
	- So $A(\theta\to\theta^*) = \min(1, r)$, the Markov chain designed with this acceptance probability will be reversible! And then has a stationary distribution as posterior

- ### Intuitively Correct? 
	- Metropolis algorithm where the proposal distribution is symmetric
		- $q(\theta|\theta^*) = q(\theta^*|\theta) \Rightarrow r = \frac{f(\theta^*)L(\theta^*|D)}{f(\theta)L(\theta|D)}$, $A(\theta\to\theta^*) = \min(1, r)$
			- If $f(\theta^*)L(\theta^*|D) > f(\theta)L(\theta|D)$, $r > 1$, $A(\theta\to\theta^*) = 1$
			- If $f(\theta^*)L(\theta^*|D) < f(\theta)L(\theta|D)$, $r < 1$, $A(\theta\to\theta^*) = r$
		- What is $f(\theta)L(\theta|D)$? – the posterior density up to a constant
			- When the proposed point $\theta^*$ has a higher density than the current point $\theta$, we will always jump to the proposed point
				- Move closer to the area of high probability! We need more samples there
			- When $\theta^*$ has a lower density than $\theta$, though, we will jump with probability equal to the ratio of their densities
				- The bigger the gap is, the less likely to go to the area of low probability
			- Most of our retained draws will be in high density regions, but we will also get some from lower density regions

- ### More on Metropolis-Hastings
	- It requires the same care as do general MCMC algorithms: multiple parallel chains, discarding warm-up/burn-in, visual and numerical diagnostics, etc. to monitor convergence to target distribution
	- Nothing in the algorithm requires $\theta$ to be one dimensional - it works for high dimension case
	- ###### Examples of proposal distribution
		- Very common like we mentioned before $q(\theta * | \theta) = N(\theta, \sigma^{2)}$ (or $\theta$* $= \theta + \Delta_{0},\Delta_{\theta}|\theta \sim N(0,\sigma^{2}$)
		- Symmetric for Metropolis, asymmetric for Metropolis-Hastings

- ### Tuning the Parameters
	- Metropolis-Hastings algorithms work better if we tune them well
		- In this example, this means picking an appropriate half-width $w$ for the Uniform proposal model
		- We want $w$ to be just right: neither too small nor too large
			- What is the problem if $w$ is too small? - Don't move too much
			- What is the problem if $w$ is too large? - Felt out to range and got rejected successively
		- In general, we want to choose a proposal distribution with a just-right variance and tail behavior, relative to the target distribution
			- Acceptance rate: 20-50% for good balance
			- Trace plot: Wandering freely
			- Check the prior
			- Adaptive tuning
			- Preliminary run to estimate the variance
		- The choice of the proposal distribution and its variance (or covariance, for multi-dimensional chains) are all part of the tuning task
		- There doesn't exist a single recipe for tuning - It is done by iterative trial-and-error