- ### CI for Population Proportion
	- ###### Bootstrap CI
		- Same approach as construction in mean problem
		- Percentile method
			- Find the $2.5^\text{th}$ and $97.5^\text{th}$ percentile from bootstrap distribution
		- Standard error method
			- Mid-point: $\hat{p}$ from the sample
			- Get standard error from bootstrap distribution
	- ###### Theoretical CI
		- Traditional CI: $\hat{p} \pm 1.96 \sqrt{\frac{\hat{p}\hat{q}}{n}}$ if large sample size (rule of thumb: at least $15$ successes and $15$ failures)
		- It doesn't perform well for extreme proportions (overall $n$ still large, but number of successes or failures small)
		- **Agresti Adjustment**: $\tilde{p} \pm 1.96 \sqrt{\frac{\tilde{p}\tilde{q}}{n+4}}$ (where $\tilde{p} = \frac{X+2}{n+4}$) (if number of successes or number of failures less than 15)
		- **Wilson Score CI**: More complicated formula

- ### A Simple Simulation
	- Nominal confidence level: $0.95$
	- **Coverage probability**: Actual likelihood the interval covers the true parameter
	- ###### For $p$ from $0$ to $1$
		- Step 1: Generate a "population" with population proportion $p$
		- Step 2: 
			- Draw a sample from the "population" ($n$ large, for example $n=100$)
			- Construct CI of $p$ based on sample (traditional, Agresti)
		- Repeat step $2$ $100$ times, and get the coverage probability
	- Compare the nominal confidence level and coverage probability ![[Pasted image 20240417002211.png]]

- ### Two Independent Samples: Proportion
	- Independent samples
	- (Designed) experiment: Treatment vs. Control
	- Not all experiments have independent groups
	- ###### Yawn example: Is yawning contagious?
		- Data: `mythbusters_yawn` (moderndive)
		- Seed group: Interviewer yawned
		- Control: Interviewer didn't
		- Observed proportion difference: $\frac{10}{34}-\frac{4}{16}=4.4$%![[Pasted image 20240417021503.png]]

- ### Bootstrapping
	- Easy with infer![[Pasted image 20240417021820.png]]
	- Resample within group (seed/control) or not?
		- Resample as a whole![[Pasted image 20240417021905.png]]

- ### Distribution of Proportion Difference
	- Add a vertical line at $x=0$![[Pasted image 20240417022004.png]]

- ### Bootstrap CI
	- Percentile method
		- `bootstrap_yawning %>% get_ci(type = "percentile", level=0.95)`
	- Standard error method
		- Is the shape of the distribution normal?
		- Specify the midpoint in CI
			- `diff_props <- mythbuster_yawn %>% specify(formula = yawn ~ group, success = "yes") %>% calculate(stat - "diff in props", order = c("seed", "control"))`
			- `bootstrap_yawning %>% get_ci(type = "se", point_estimate = diff_props)`

- ### Theoretical CI
	- Traditional: $(\hat{p}_{1} - \hat{p}_{2)}\pm 1.96 \sqrt{\frac{\hat{p}_{1}\hat{q}_{1}}{n_{1}}+ \frac{\hat{p}_{2}\hat{q}_{2}}{n_2}}$
	- Agresti:
		- $\tilde{p}_1 = \frac{x_{1}+1}{n_{1}+2}$, $\tilde{p}_2=\frac{x_{2}+1}{n_{2}+2}$
		- $\tilde{p}_{1}- \tilde{p}_{2}\pm \sqrt{\frac{\hat{p}_{1}(1 - \hat{p}_{1})}{n_{1}+2}+ \frac{\hat{p}_{2}(1-\hat{p}_{2})}{n_{2}+2}}$

- ### Summary / Comparison of CI
	- 4 pairs of CI![[Pasted image 20240417024454.png]]
	- Standard error method vs. traditional CI
	- Traditional CI vs. Agresti adjustment
		- Number of successes and failures large enough?
	- How so we interpret CI?
		- Is 0 in the CI?

- ### Two Independent Samples: Mean
	- Example: Teaching score evaluation
		- `bootstrap_evals <- evals %>% select(score, gender) %>%  specify(formula = score ~ gender) %>% generate(reps = 1000, type = "bootstrap") %>% calculate(stat = "diff in means", order = c("male","female"))`
	- Bootstrap distribution ![[Pasted image 20240417030312.png]]

- ### CI: Mean difference
	- Bootstrap CI
		- Same approach
	- ###### Theoretical CI
		- $(\bar{x}_{1} - \bar{x}_{2})\pm 1.96 \sqrt{\frac{s^{2}_1}{n_{1}}+\frac{s^{2}_2}{n_{2}}}$
		- More complicated formula involving variance estimation
	- Summary / comparison of CI![[Pasted image 20240417031351.png]]

- ### CI: More
	- ###### Interpret the CI
		- 0 in CI?
		- Difference between female mean score and male mean score?
	- Regression results![[Pasted image 20240417031554.png]]
	- Do they tell the same story?
	- ###### What does CI depend on?
		- Will the center of CI change?
			- Percentile method: Might change, but slightly
			- Standard error method, Theoretical CI
				- Shouldn't change
				- Centered at $\hat{p}$, $\bar{x}$, etc.
				- Symmetric
		- How about the width?
			- The higher the confidence level, the wider the CI
			- The larger the sample size, the narrower the CI
	- ###### More Discussions
		- Theoretical CI
			- Parametric method, need to check assumptions
			- When sample size small, there are additional methods
				- Use of $t$ distribution
				- Use of binomial distribution
			- Could have the case: nowhere to start
		- Bootstrap CI
			- Nonparametric or combination
			- Standard error method: need to check assumptions
			- Could work for large or small sample size
			- Sample size should be "large enough"
			- Be careful about extreme value
			- Could have the case: nowhere to start