
- ### Example: Promotion
	- ###### $48$ bank supervisors each evaluated a resume (*identical* except name) and gave their recommendations for promotion or not
		- $24$ female names, $24$ male names
		- Randomly assigned to supervisors
		- Saved in "promotions" (moderndive)
		- Is there gender discrimination in promotion?
	- Distribution![[Pasted image 20240417221034.png]]
	- ###### Promotion rate
		- Overall: $\frac{35}{48}=72.9$%
		- Female: $\frac{14}{24}=58.3$%
		- Male: $\frac{21}{24}=87.5$%
		- Observed difference: $87.5$%$-58.3$%$=29.2$%
	- Formulating hypothesis
	- Significance level
	- Calculating test statistic or $p-$value
		- When the null hypothesis is true...
	- Under $H_0$ what will we observe?
		- No gender discrimination: Proportion of male who got promoted be the same as proportion of female who got promoted
		- Equal size of male and female in the data
		- Overall $35$ got promoted
		- Roughly equal number of male and female who got promoted?

- ### Manual Shuffling
	- ###### Standard deck of $52$ cards
		- Half red - female
		- Half black - male
	- $48$ total observations - get rid of 2 red and 2 black
	- Need to be in random order - shuffle the cards
	- ###### Results
		- For each resume, turn over the card
			- If it is red, `shuffled_gender="female"`, otherwise `"male"`
		- Shuffle once results: `promotions_shuffled` (moderndive)
			- Proportion difference: $\frac{18}{24}-\frac{17}{24}=4.17$%
		- Plot![[Pasted image 20240417224012.png]]

- ### Shuffling 16 times
	- Could be randomness with one shuffle
	- We can get the distribution of the proportion difference under $H_0$ if we shuffle more times
		- $16$ shuffles results: `ch10_gender_promotions_results.csv` (in project folder)
		- What the distribution looks like?
		- Where is the relative position of our observed difference?
		- How likely to observe it?![[Pasted image 20240417224432.png]]

- ### Virtual Shuffling
	- Let computer do it
		- `generate(reps=1000, type="permute")`
	- ###### Called hypothesis testing using a permutation method
		- Why is it called "permutation"
			- Rearrangement of the labels on observed data points
	- ###### Resampling technique
		- Resample from the observed sample
		- Draw without replacement
			- Why without replacement?
	- Infer package![[Pasted image 20240417224812.png]]

- ### Infer Promotion Example
	- Generate sampling distribution under the null
		- `null_promotions <- promotions %>% specify(formula=decision~gender, success="promoted") %>% hypothesize(null="independence") %>% generate(reps=1000, type="permute") %>% calculate(stat="diff in props", order=c("male", "female"))`
	- Observed sample proportion difference
		- `diff_props <- promotions %>% specify(formula=decision~gender, success="promoted") %>% calculate(stat="diff in props", order=c("male", "female")`

- ### Sampling Distribution (Under Null)
	- Get sampling distribution and shade $p-$value
		- `visualize(null_promotions, bins=10) + shade_p_value(obs_stat = diff_props, direction = "right")`
	- What the distribution looks like? Centered at $0$? ![[Pasted image 20240417231409.png]]

- ### P-value and Conclusion
	- ###### Calculate $p-$value
		- `null_promotions %>% get_p_value(obs_stat = diff_props, direction = "right")`
		- $p=0.023 < 0.005$ reject null
		- Is the observed difference due to random chance or is there gender discrimination?

- ### More about HT
	- ###### What does conclusion depend on?
		- The significance level
		- Whether it is one tailed or two tailed
			- Two tailed test $p-$value (same data)
				- Doubles one-tailed $p-$value (when one tailed $p-$value $< 0.5$)
				- Doubles ($1 -$ one tailed $p-$value)
	- Hypotheses and significance level should be determined *before* you see the data

- ### Teaching Score
	- Are there significant difference between average female faculty teaching score and average male faculty teaching score?
	- Hypothesis
		- One tailed or two tailed
	- Get distribution under null
		- `null_evals <- evals %>% specify(formula = score~gender) %>% hypothesize(null = "independence") %>% generate(reps=1000, type="permute") %>% calculate(stat = "diff in means", order=c("male", "female"))`

- ### Sampling Distribution under Null and P-Value
	- Distribution![[Pasted image 20240418004552.png]]
	- ###### $p-$value
		- `null_evals %>% get_p_value(obs_stat = diff_means, direction = "two-sided")`
		- $p=0.01$
	- We can reject

- ### CI and HT Comparison
	- Do they tell the same story ![[Pasted image 20240418004822.png]]

- ### One Sample HT
	- Are college instructors below average looking?
	- Hypothesis
	- Get distribution under null
		- `null_evals <- evals %>% specify(response = bty_avg) %>% hypothesize(null = "point") %>% generate(reps=1000, type="bootstrap") %>% calculate(stat = "mean")`
	- Sampling distribution ![[Pasted image 20240418005107.png]]
	- ###### $p-$value
		- `null_evals %>% get_p_value(obs_stat = sample_mean, direction = "left")`
		- $p=0$

- ### One Sample HT: More
	- Are there more than $70$% employees who got  promoted?
	- Get distribution under null
		- `null_promotions <- promotions %>% specify(response = decision, success = "promoted") %>% hypothesize (null = "point", p=0.7) %>%  generate(reps = 1000, type = "draw") %>% calculate(stat = "prop")`
	- Distribution![[Pasted image 20240418005412.png]]
	- ###### $p-$value
		- `null_promotions %>% get_p_value(obs_stat = sample_prop, direction = "right")`
		- $p=0.39$

- ### Summary of Resampling Types
	- `type="bootstrap"`
		- A bootstrap sample will be drawn for each replicate
		- With replacement
		- For CI and HT for one sample mean
	- `type="permute"`
		- Each input value will be randomly reassigned to a new output value for each replicate
		- Without replacement
		- For HT for two sample mean (proportion) difference
	- `type="draw"`
		- A value will be sampled from a theoretical distribution (with parameter $p$) for each replicate
		- For HT for one sample proportion