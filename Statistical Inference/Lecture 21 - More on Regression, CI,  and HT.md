
- ### HT in Regression
	- ###### Regression Model
		- $y=\beta_{0}+\beta_{1}x + \epsilon$
		- $\hat{y}=\hat{\beta_{0}}+\hat{\beta_{1}}x + \epsilon$
	- Distribution of $\hat{\beta_{1}}$
		- With the same assumption of random error, the sampling distribution of the slope $\hat{\beta_{1}}$ will be normal with the mean $\hat{\beta_{1}}$ (the true slope)
	- ###### Why do we want to test whether the true slope is $0$
		- Does $x$ have contribution to the prediction of $y$?
		- If slope is $0$, $x$ is completely unrelated to $y$, and there is no linear relationship
	- ###### One-tailed or two-tailed test
		- One tailed: $H_{0}:\beta_{1}=0$ vs. $H_{a}:\beta_{1} < 0$ (or $\beta_{1} > 0$)
		- Two tailed: $H_{0} : \beta_{1}=0$ vs. $H_{a}:\beta_{1} \ne 0$
	- ###### Test statistic
		- `test stat` = estimate / standard error
		- Because of the distribution of beta coefficient
		- It is a $t$ test
	- ###### $p-$value of the test
		- The reported $p-$value is for two tailed test
		- What if we have a one tailed test?
			- If $H_{a}:\beta_{1}>0$
				- If $t>0$, then $p-$value $= \frac{p}{2}$
				- If $t<0$, then $p-$value $=1-\frac{p}{2}$
			- If $H_{a}:\beta_{1} < 0$
				- If $t<0$, then $p-$value $=\frac{p}{2}$
				- If $t>0$, then $p-$value $=1- \frac{p}{2}$
	- ###### If we are interested in testing: the higher the beauty score, the higher the teaching score?
		- What is the alternative?
		- What is the $p-$value of the test?

- ### CI in Regression
	- ###### `lower_ci` and `upper_ci`
		- They are the $95$% CI for the true beta coefficient
		- They are calculated as `estimate` $\pm$ $t_{\frac{a}{2}} *$ `standard error`
		- What if we want to have a different confidence level
			- Change the critical value from $t$ distribution
	- ###### Model of teaching score on beauty score
		- $95$% CI of $\beta_{1} = (0.035, 0.099)$
		- Is it consistent with $p-$value?

- ### HT and CI in Multiple Regression
	- Conducted the same way
	- `MSE`, `RMSE`, `sigma`, `statistic`, `p_value`, `df`
		- Related with $f$ test

- ### F Test in Multiple Regression
	- ###### Hypothesis
		- $H_{0}:\beta_{1}=\beta_{2}=\dots=\beta_{k}=0$
		- $H_{a}:$ At least of one the $\beta$s $\ne 0$
	- ###### What is the $f$ test?
		- A single test for the overall model
		- It involves ANOVA table
	- ###### In multiple regression
		- Regression table: $t$ test is for each *individual coefficient*
		- Regression summary: $f$ test is for *overall* usefulness of the model
		- It could be possible that the final model has regressors with insignificant $t$ statistics, but the overall $f$ is significant
			- Ex. Interaction significant but the main terms aren't multicollinearity
	- ###### In simple regression
		- $t$ test (for the slope) and $f$ test are equivalent

- ### One Way ANOVA
	- Analysis of variance
	- Response variable $y$, at different groups
		- Ex. Teaching scores at 3 ranks (teaching, tenured, tenure track)
	- ###### Conditions
		- The samples are independently and randomly selected from the population
		- All sampled populations are approximately normally distributed
		- The population variances are same for all treatment groups
	- ANOVA is robust
	- ###### Hypothesis (testing the population mean in groups)
		- $H_{0}:\mu_{1}=\mu_{2}=\dots=\mu_{k}$
		- $H_{a}:$ At least two of the $k$ treatment means differ
	- Test statistic
		- $f$ test, $p-$value from $f$ table

- ### Testing Population Means
	- Check difference between the treatment means
	- Check variability between treatment groups
	- When either is relatively large, there is likely a real difference

- ### ANOVA Table
	- Table![[Pasted image 20240425223705.png]]
	- ###### SS: Sum of Squares 
		- **SSTr**: Sum Square of Treatment (SS Between)
		- **SSE**: Sum Square of Error (SS Within)
	- **MS**: Mean Squares
	- **$f$ statistic**
		- It has two degrees of freedom
	- ANOVA table in multiple group comparison and ANOVA table in regression

- ### ANOVA in R
	- Simple R function
		- `test1<-aov(data=evals, score~rank)` `summary(test1)`
	- ###### Infer package
		- `Ftest <- evals %>% specify(formula= score ~ rank) %>%  hypothesize(null = "independence") %>% calculate(stat = "F") Ftest`
		- Need $p-$value from test stat
	- ###### Equivalent Results
		- Sample mean from each group vs. regression coefficients
		- $f$ test in ANOVA and $f$ test in regression
	- ANOVA is equivalent to regression of response on a categorical variable

- ### ANOVA when $k=2$
	- ANOVA is equivalent with regression
	- ###### Two sample test $H_{0}:\mu_{1}-\mu_{2}=0$
		- $z$ test for large sample
		- Pooled $t$ test
		- ANOVA $f$ is equivalent to two tailed $t$ test
	- CI and HT
		- Mean problem, CI is equivalent to two tailed test

- ### More on ANOVA
	- ###### One way ANOVA
		- Completely randomized design
		- Randomized block design
		- Multiple comparison
	- ###### Two way ANOVA
		- Interaction model