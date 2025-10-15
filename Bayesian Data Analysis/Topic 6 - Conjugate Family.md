
- ### Poisson Distribution
	- Describing the number of events that will occur in a specific period of time
		- The number of events that occur in one unit of time is independent of the number that occur in any other mutually exclusive unit
	- Example: $X \sim \text{Pois}(\lambda)$
	- PMF: $p(x)=\frac{\lambda^xe^{-\lambda}}{x!}$ where $x=0,1,2\dots$
	- ###### Properties of Poisson Distribution
		- Mean and Variance: $\mu=\sigma^2=\lambda$
		- The sum of independent Poisson is still Poisson
			- If $X \sim \text{Pois}(\lambda_{1}),Y\sim \text{Pois}(\lambda_{2})$, and $X \perp Y$, then $X+Y \sim \text{Pois}(\lambda_{1}+\lambda_{2})$
		- Shape of the Poisson density
			- Right skewed
			- As $\lambda$ gets larger, the shape is more bell shaped symmetric

- ### Likelihood of Lambda Given Data
	- Let $y_{1},y_{2},\dots,y_{n}$ be the number of fraud risk phone calls on each of the $n$ sampled days. Assume that they all can be independently modeled by the Poisson. That is, on each day $i$, $y_{i}|\lambda \text{iid} \sim \text{Pois}(\lambda)$
	- PMF $f(y_{i}|\lambda)=\frac{\lambda^{y_i}e^{-\lambda}}{y_{i}!}$
		- The sum of independent Poisson is still Poisson, therefore we can use the PMF for Poisson but use $y_{i}$ for $x$ to calculate Poisson for each day
	- ###### Joint Probability Function
		- $f(\vec{y} \mid \lambda) = \prod_{i=1}^{n} f(y_i \mid \lambda) = f(y_1 \mid \lambda) \cdot f(y_2 \mid \lambda) \cdots f(y_n \mid \lambda)$
		- $f(\vec{y} \mid \lambda)= \prod_{i=1}^{n} \frac{\lambda^{y_i} e^{-\lambda}}{y_i!} = \frac{\lambda^{\sum y_i} e^{-n\lambda}}{\prod y_i!} \propto \lambda^{\sum y_i} e^{-n\lambda}$
		- The likelihood depends on the data only through the mean and the sample size
	- Kernel of the likelihood function: $\lambda^{\sum y_{i}}e^{-n\lambda}$

- ### Gamma Distribution
	- Gamma with *shape* parameter $\alpha$ and *scale* parameter $\beta$
		- $f(x;\alpha,\beta)=\frac{1}{\Gamma(\alpha)\beta^{\alpha}}x^{\alpha-1}e^{-x/\beta}$ where $x>0$
		- Directly describes how stretched the data is
		- Often used when you're more interested in the time until an event happens
	- Gamma with *shape* parameter $s$ and *rate* parameter $r$
		- $f(x;s,r)=\frac{r^2}{\Gamma(s)x^{s-1}e^{-r}}$ where $x>0$
		- Often used when you're dealing with frequencies or rates of events (e.g. number of events per unit time)
		- Describes how fast the distribution "decays" or concentrates
	- The *scale* parameter and the *rate* parameter are inversely related
	- ###### Two special Gamma
		- Exponential: A special Gamma with shape $=1$
		- Chi-square with df $k$: A special Gamma with shape $=k/2$, scale $=2$

- ### Properties of Gamma Distribution
	- Mean, Mode, and Variance of Gamma$$
\begin{array}{|c|c|c|c|}
\hline
 & \textbf{Mean} & \textbf{Mode} & \textbf{Variance} \\
\hline
\text{shape } \alpha \text{ scale } \beta 
& \alpha \beta 
& 
\begin{cases}
(\alpha - 1)\beta, & \text{if } \alpha \ge 1 \\
0, & \text{if } \alpha < 1
\end{cases}
& \alpha \beta^2 \\
\hline
\text{shape } s \text{ rate } r 
& \dfrac{s}{r}
& 
\begin{cases}
\dfrac{s-1}{r}, & \text{if } s \ge 1 \\
0, & \text{if } s < 1
\end{cases}
& \dfrac{s}{r^2} \\
\hline
\end{array}
$$
	- If $X \sim \text{Gamma}(s_{1},r), Y\sim \text{Gamma}(s_{2},r)$ and $X \perp Y$, then $X+Y \sim \text{Gamma}(s_{1}+s_{2},r)$
	- If $X \sim \text{Gamma}(s,r)$ and $c$ is a constant, then $\frac{X}{c}\sim \text{Gamma}(s,r\cdot c)$
	- ###### Relationship with Poisson
		- A Poisson process with parameter $\lambda$
		- The waiting time until one occurrence is exponential with rate $\lambda$
		- The waiting time until $s$ occurrences is Gamma with shape $s$ and rate $\lambda$

- ### Shape of the Gamma Density
	- When shape $s>1$
		- Unimodal, somewhat bell shaped, right skewed
		- The larger the shape the more like normal
			- With same rate, the larger the shape, the larger the variance
		- The larger the rate, the more compressed
			- With same shape the larger the rate, the smaller the variance
	- When shape $s=1$
		- Exponential decay
		- The larger the rate parameter is, the rapidly the decay is
	- When shape $s<1$
		- Density approaches infinity as $x\rightarrow 0^+$, and decrease rapidly as $x$ increases, highly right skewed, high concentration near $0$
			- With same rate, the smaller the shape, the more rapid the decay
			- With same shape, the larger the rate, the more rapid the decay

- ### Gamma - Poisson Family
	- Prior: $\lambda \sim \text{Gamma}(s,r)$
		- Density: $f(\lambda)=\frac{r^s}{\Gamma(s)}\lambda^{s-1}e^{-r\lambda}$ where ($\lambda>0$)
	- Data: $y|\lambda \sim \text{Pois}(\lambda)$
		- Likelihood: $L(\lambda|y) \propto \lambda^{\sum y_{i}}e^{-n\lambda}$
	- ###### Posterior density
		- $f(\lambda|\vec{y})\propto \lambda^{\sum y_{i}}e^{-n\lambda} \cdot \lambda^{s-1}e^{-r\lambda} = \lambda^{s+\sum y_{i}-1}e^{-(r+n)\lambda}$
		- This is the kernel of Gamma distribution with parameters $s + \sum y_{i}$ and $r+n$
		- The posterior $\lambda|y \sim \text{Gamma}(s+\sum y_{i},r+n)$ or $\lambda|y \sim \text{Gamma}(s+n\bar{y},r+n)$
		- The normalizing constant is $\frac{(r + n)^{s + n\bar{y}}}{\Gamma(s + n\bar{y})}$
		- Density of posterior: $\frac{(r + n)^{s + n\bar{y}}}{\Gamma(s + n\bar{y})} \lambda^{s + n\bar{y} - 1} e^{-(r + n)\lambda}$
		- This is called Gamma-Poisson conjugacy

- ### Properties of Gamma - Poisson Family
	- ###### Posterior mean
		- $\frac{s+n\bar{y}}{n+r}=\frac{s}{n+r}+\frac{n\bar{y}}{n+r}=\frac{r}{n+r}\cdot \frac{s}{r}+\frac{n}{n+r}\cdot \bar{y}$
			- Posterior mean is the weighted average of the prior mean and data mean
			- When $n >> r$ (heavy data) the posterior mean will be dominated by data mean
			- When $r >> n$ ($\frac{s}{r^2}$ close to $0$, heavy prior), the posterior mean will be dominated by the prior mean
	- Posterior mode: $\frac{s+n\bar{y}-1}{n+r}$
		- $\frac{s+n\bar{y}-1}{n+r}=\frac{r}{n+r}\cdot \frac{s-1}{r}+\frac{n}{n+r}\cdot \bar y$
		- Posterior mode is the weighted average of the prior mode and data mean
	- Posterior variance: $\frac{s+n\bar y}{(n+r)^2}$

- ### How to Choose Gamma Parameters
	- Fraud risk calls: Prior to collecting any data, guess was that the rate $\lambda$ was most likely around 5 calls per day but could also reasonably range between 2 calls and 7 calls
	- $E(\lambda)=\frac{s}{r}\approx 5$
	- Majority of the value of Gamma between 2 and 7![[Pasted image 20251004192422.png]]

- ### Normal Distribution
	- Normal distribution with parameters $\mu$ and $\sigma^2$: $X \sim N(\mu,\sigma^2)$
		- Bell shaped, symmetric curve
		- Also called Gaussian distribution
		- Most prominent probability distribution
		- Many phenomena generate random variables that are approximately normal
	- PDF: $f(x)=\frac{1}{\sqrt{2\pi\sigma^2}}\text{exp}(-\frac{(x-\mu)^2}{2\sigma^2})$, where $y \in \mathbb{R}$
	- Gaussian integral: $\int_{-\infty}^{\infty}e^{-x^2}=\sqrt{\pi}$
	- $E(X)=\mu,V(X)=\sigma^2$
	- When $\mu=0$, $\sigma=1$, it is called standard normal $Z=N(0,1)$
		- Normal transformation $Z=\frac{X-\mu}{\sigma}\sim N(0,1)$

- ### Properties of Normal PDF
	- ###### The sum of independent normal is still normal
		- If $X \sim N(\mu_1, \sigma_1^2)$, $Y \sim N(\mu_2, \sigma_2^2)$, and $X \perp Y$, then $X + Y \sim N(\mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)$
		- If $X_i$ iid $\sim N(\mu, \sigma^2)$, then $\bar{X} \sim N(\mu, \frac{\sigma^2}{n})$
	- ###### Shape of the normal: bell shaped symmetric
		- Centered at mean = median = mode = $\mu$
		- Points of inflection at $x=\mu \pm \sigma$
		- The larger the $\sigma$ is, the flatter the bell
	- Empirical rule
		- Roughly 68%, 95%, 99.7% of $x$ values will be within 1, 2, 3 standard deviations of its mean (i.e. $\mu \pm \sigma, \mu \pm 2\sigma, \mu \pm 3\sigma$)

- ### Likelihood of Mu Given Data
	- Let $y_1, y_2, \cdots, y_n$ be the volume of the hippocampus of the n sampled patients. Assume that they all can be independently modeled by normal distribution with same $\mu$ and $\sigma^2$. That is, $y_i|\mu$ iid $\sim N(\mu, \sigma^2)$
	- PDF $f(y_i|\mu) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(y_i-\mu)^2}{2\sigma^2}\right)$ (Assuming $\sigma^2$ known)
	- ###### Joint probability function
		- $f(\vec{y}|\mu) = \prod_{i=1}^{n} f(y_i|\mu) = f(y_1|\mu) \cdot f(y_2|\mu) \cdots f(y_n|\mu)$
		- $= \prod \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(y_i-\mu)^2}{2\sigma^2}\right)$
		- $\propto \exp\left(-\frac{\sum(y_i-\mu)^2}{2\sigma^2}\right) \cdots \propto \exp\left(-\frac{(\bar{y}-\mu)^2}{2\sigma^2/n}\right)$
		- The likelihood depends on the data only through the mean and sample size
	- Kernel of the likelihood function: $\text{exp}(-\frac{(\bar{y}-\mu)^2}{2\sigma^{2}/n})$

- ### Normal - Normal Family
	- Prior: $\mu \sim N(\theta,\tau^2)$
		- Density: $f(\mu)=\frac{1}{\sqrt{2\pi\tau^{2}}}\text{exp}(-\frac{(\mu-\theta)^2}{2\tau^2})$
	- Data: $y|\mu \sim N(\mu,\sigma^{2})$
		- Likelihood: $L(\mu|y)\propto \text{exp}(-\frac{(\bar{y}-\mu)^2}{2\sigma^2/n})$
	- ###### Posterior density
		- $f(\mu|\vec{y}) \propto \exp\left(-\frac{(\mu-\theta)^2}{2\tau^2}\right) \exp\left(-\frac{(\bar{y}-\mu)^2}{2\sigma^2/n}\right) \cdots \propto \exp\left(-\frac{(\mu-\theta_n)^2}{2\tau_n^2}\right)$
		- $\theta_n = \frac{\frac{1}{\tau^2}}{\frac{1}{\tau^2}+\frac{n}{\sigma^2}} \theta + \frac{\frac{n}{\sigma^2}}{\frac{1}{\tau^2}+\frac{n}{\sigma^2}} \bar{y}, \quad \frac{1}{\tau_n^2} = \frac{1}{\tau^2} + \frac{n}{\sigma^2}$
		- The normalizing constant is $\frac{1}{\sqrt{2\pi\tau_n^2}}$
		- Density of posterior: $\frac{1}{\sqrt{2\pi\tau_n^2}} \exp\left(-\frac{(\mu-\theta_n)^2}{2\tau_n^2}\right)$
		- This is called Normal-Normal conjugacy

- ### Property of Normal - Normal Family
	- The reciprocal of the variance is called the precision
	- Posterior precision is the sum of prior precision and data precision
		- $\frac{1}{\tau^2_n}=\frac{1}{\tau^2}+\frac{n}{\sigma^2}$
		- Information adds linearly in terms of precision
	- Posterior mean is the weighted average of the prior mean and data mean
	- $\theta_n = \frac{\frac{1}{\tau^2}}{\frac{1}{\tau^2}+\frac{n}{\sigma^2}} \theta + \frac{\frac{n}{\sigma^2}}{\frac{1}{\tau^2}+\frac{n}{\sigma^2}} \bar{y}$
	- $\text {posterior mean}$ $=$ $\frac{\text{prior precision}}{\text{posterior precision}}$ $\text {prior mean}$ $+$ $\frac{\text{data precision}}{\text{posterior precision}}$ $\text{data mean}$
		- Prior and data contribute to the posterior proportionally to their precision
	- When $n$ sufficiently large (heavy data), posterior mean is dominated by the data mean
	- When $\tau^2$ sufficiently small (heavy prior), posterior mean is dominated by the prior mean

- ### Summarizing Posterior
	- The posterior tells us everything we know about a parameter, but we would like to have ways of summarizing it
	- Measure of central tendency: variance, SD
	- ###### Credible intervals
		- The Bayesian counterpart to confidence intervals
		- Incorporate both location and spread of the posterior
		- If a 90% credible interval $\rightarrow$ there is a 90% probability that the parameter is in the 90% credible interval
		- Credible intervals are often given as 90% instead of 95%, in part because the boundaries of a 90% credible interval are more stable than the boundaries of a 95% credible interval
		- **Central posterior credible interval**
			- 90%: simply find the points corresponding to the 5th and 95th percentiles of the posterior, so equal tail probability
			- You can get somewhat disconcerting results
		- **Highest posterior density (HPD) credible interval**
			- 90%: all values of $\theta$ such that the probability density of $\theta$ is greater than or equal to $w$, where $w$ is defined such that $\int_{\theta:p(\theta)\geq w} p(\theta)d\theta = 0.9$
			- Every point in the HPD interval has a higher probability than every point outside it
			- The HPD interval is harder to calculate than the central posterior credible interval (use R) 
			- For a multi-modal distribution, the HPD may consist of separated regions
		- For roughly symmetric posteriors, the equal tails and the HPD credible intervals will be very close to the same