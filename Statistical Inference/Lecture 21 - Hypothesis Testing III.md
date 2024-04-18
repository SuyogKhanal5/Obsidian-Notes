
- ### Problem Types
	- Diagram![[Pasted image 20240418130715.png]]

- ### Paired Samples
	- Two dependent samples
	- ###### Typically
		- **Natural Pairs**: Comparing the scores of two subjects that are related naturally (ex. Twins)
		- **Matched Pairs**: Pairs two groups of subjects on some characteristic that is likely to be important to the variable which you are studying (ex. Married couples)
		- **Repeated Measures**: Same people at two different times of measure (of the same variable) (ex. pretest/posttest)
	- ###### Advantages
		- Less cost/labor
		- Control for confounding factors

- ### Paired Samples Inferences
	- Ideally data in the format
		- `ID`     `sample1`      `sample2`
	- Create a new variable `diff=sample1-sample2`
	- *One sample* approach based on new diff variable
	- ###### Example
		- Zinc concentration in bottom water and surface water at $10$ randomly selected locations on a stretch of river
		- Why paired sample?
		- Which type?

- ### Zinc Concentration Data
	- Data![[Pasted image 20240418154336.png]]
	- Get the paired difference
		- `zinc_diff <- zinc_tidy %>% group_by(loc_id) %>% summarize(pair_diff = diff(concentration))`

- ### Zinc Concentration: CI
	- Bootstrap distribution![[Pasted image 20240418163206.png]]
	- CI
		- Theoretical CI is based on $t$ distribution with $df=9$![[Pasted image 20240418163300.png]]

- ### Zinc Concentration: HT
	- Is the concentration in the surface water smaller than that of bottom water?
	- One or two tailed?
	- Distribution under the null![[Pasted image 20240418165322.png]]
	- $p=0$

- ### Theoretical HT
	- ###### Population mean problem
		- Parametric test
			- $Z$ test or $t$ test
			- Large sample, sample mean will be approximately normally distributed
			- Small sample, assume the population is normally distributed
		- Non-parametric test
			- No normal assumption
			- Wilcoxson signed test
			- Wilcoxson rank sum test
	- ###### Population proportion problem
		- $Z$ test for large sample
		- Small sample test based on binomial distribution
	- Formulas![[Pasted image 20240418165618.png]]
	- ###### Wilcoxson tests
		- Based on the ranks of observations
		- When sample size large enough, Wilcoxson tests have normal approximation
	- ###### $p-$value from theoretical tests
		- From normal table, $t$ tables, Wilcoxson tables
		- `pnorm` function
	- ###### Theoretical test stat can be calculated in $R$
		- Mean test: $t$ test
		- Proportion test: $z$ test
		- But need to check whether conditions are satisfied

- ### Calculate Theoretical Test Stat
	- ###### Two sample proportion difference
		- Note: One cell only have 3 observations
		- `ztest <- promotions %>% specify(formula = decision ~ gender, success = "promoted") %>% calculate(stat = "z", order = c("male", "female"))`
	- ###### Two sample mean difference
		- `ttest <- evals %>% specify(formula = score ~ gender) %>%  calculate(stat = "t", order = c("male", "female"))  2*pnorm(ttest$stat, 0,1, lower.tail=FALSE)`
	- ###### One sample mean
		- `ttest <- evals %>% specify(response = bty_avg ) %>%  hypothesize(null="point", mu=5) %>% calculate(stat = "t")  pnorm(ttest$stat,0,1,lower.tail=TRUE`
	- ###### One sample promotion
		- `ztest <- promotions %>% specify(response = decision , success = "promoted") %>% hypothesize(null="point", p=0.7) %>%  calculate(stat = "z")`

- ### Theoretical CI and HT
	- ###### Population mean problem and two tailed test
		- HT and CI are equivalent
		- $H_{0} : \mu = \mu_{0}$ vs. $H_{a}: \mu \ne \mu_0$
			- If $\mu_0$ is in CI, then fail to reject the null
		- $H_{0} : \mu_{1}- \mu_{2} = 0$ vs. $H_{a} : \mu_{1} - \mu_{2} \ne 0$
			- If $0$ is in CI, then failure to reject the null
	- ###### Population mean problem and one tailed test
		- HT and CI are not equivalent, but HT is equivalent to one way confidence bound
	- ###### Population proportion problem
		- Even for two tailed test, HT and CI are not equivalent but often show consistent results
		- One tailed test, HT and one way confidence bound are not equivalent but often show consistent results

- ### Testing Non-zero in Two Sample Difference
	- ###### Theoretical test
		- Mean test
		- Proportion test
			- $p-$value
	- ###### Replication/simulation test
		- Ex. Transformations
			- `score2 = ifelse(gender=="male", score-0.1, score)`
	- Using CI