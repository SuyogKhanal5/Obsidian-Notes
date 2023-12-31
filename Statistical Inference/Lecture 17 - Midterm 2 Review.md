
- ### What we have learned
	- ###### Multiple Regression
		- One numerical and one categorical
		- Two numerical
		- Quadratic regression
		- Collinearity
		- Extrapolation
	- ###### Simpson's Paradox
		- In contingency table
		- In regression
	- ###### Sampling
		- Population parameter vs. Sample statistic
		- Sampling distribution
	- Bootstrapping
	- Central Limit Theorem

- ### Multiple Regression
	- ###### One Numerical and One Categorical
		- Parallel slope
			- $E(y)=\beta_{0}+\beta_{1}x_{1}+\beta_{2}x_{2}$ where $x_{2}$ is dummy
			- Interpret $\beta$ as coefficient
			- Compare $\beta_{1}$ to that in $E(y)=\beta_{0}+\beta_{1}x_{1}$
		- Separate slope
			- $E(y)=\beta_{0}+\beta_{1}x_{1}+\beta_{2}x_{2}+\beta_{3}x_{1}x_{2}$ where $x_{2}$ is dummy
		- How to know which to use?
			- Run it with interaction, if $\beta_{3}$ is not significant, we run parallel slope
			- When we run two parallel slope model regressions separately, the two slopes are not necessarily the same
	- ###### Two Numerical
		- No interaction
			- $E(y)=\beta_{0}+\beta_{1}x_{1}+\beta_{2}x_{2}$
			- Interpret $\beta$ coefficient
			- Compare coefficient to those in individual simple regression
			- Flat regression plane, parallel contour plot
		- Separate slope
			- $E(y)=\beta_{0}+\beta_{1}x_{1}+\beta_{2}x_{2}+\beta_{3}x_{1}x_{2}$
			- Interpret $\beta$ coefficient
			- Significancy of the interaction term ($\beta_{3}$)
			- Twisted regression plane, non parallel contour plot
		- If nothing is significant, $y=x_{1}$
	- ###### Quadratic Model
		- Check the scatterplot to see whether there is a curve
		- $E(y)=\beta_{0}+\beta_{1}x+\beta_{2}x^{2}$
		- Need to create the square term first
		- Add quadratic curve on histogram
		- Interpret $\beta$ coefficient
			- Does parabola open up or down?
	- ###### In General
		- Assumptions
			- Same as simple regression
		- Fitted values and residuals
			- Same approach as simple regression
		- $R^{2}$ and adjusted $R^{2}$
			- Adjusted $R^{2}$ takes into account the number of regressors and number of observations
			- $R^{2}$ fails in multiple regression since it will always go up the more variables you add, no matter how bad they are
		- Overall significancy and individual effect
		- Extrapolation
			- Avoid it as much as possible
			- Add disclaimer: "If $\dots$ keeps the same pattern $\dots$"

- ### Collinearity/Multicollinearity
	- ###### Detecting Collinearity
		- Significant correlation between pairs of independent variables
		- Significant overall but insignificant for some parameters
		- $\beta$ coefficient signs opposite from expected
	- ###### What to do
		- Make inference
			- Can't have it
		- Make estimation/prediction
			- Can let it go

- ### Simpson's Paradox
	- ###### In contingency table
		- Berkeley admissions
	- ###### In regression
		- Median Housing Prices vs. Average Distance to Employment Centers in Boston Housing Data
	- ###### Hidden Third Variable
		- Berkeley: Department applied to
		- Boston: Zoning status
	- The results at aggregated level could be different of those at the hidden variable

- ### Sampling
	- ###### Population vs. Sample
		- We can't get full population so we need representative sample
	- ###### Sampling
		- Get a sample from the population
		- Goal: A representative sample
	- Draw with replacement vs without replacement
	- Sampling Design
	- ###### Things to avoid
		- Selection bias
		- Nonresponse bias
	- ###### Sampling Distribution
		- Population parameter vs. Sample statistics
		- Point estimate
			- It is used to estimate the population parameter
			- It is a random variable
			- It has a distribution
			- It is not enough
	- ###### Sample Distribution vs. Sampling Distribution and Standard Deviation vs. Standard Error
		- Sample distribution, standard deviation
			- For those observed in the sample
				- Ex. Individual height, male/female status
		- Sampling distribution, standard error
			- For those calculated sample statistics (sample mean/proportion)
				- Ex. Average height, proportion of female
	- ###### Sampling vs Resampling
		- Sampling
			- Purpose: Get mean and standard error of sample statistic
			- Random sample from population
			- Draw without replacement
			- No duplicates
			- Any sample size
			- Sampling Distribution
		- Bootstrapping
			- Purpose: Get mean and standard error of sample statistic
			- Random sample from a single observed sample
			- Draw with replacement
			- Could have duplicates in a sample
			- Sample size needs to be the same as that in the initial sample
			- Bootstrap distribution
		- Which one is more realistic?  
			- Do we know the population?  
		- Which one is more time consuming?  
			- Sampling  
				- For each sample, need to get the sample results  
				- There could be duplicates across samples, not necessarily \# repeats * unit time for one sample  
			- Bootstrapping  
				- Once the initial sample is got, can use computer to draw with  
				replacement  
		- Why did we compare sampling distribution / bootstrap distribution / theoretical distribution in shovel example  
			- How do we know which one is good?  
			- Will bootstrapping always have good results?

- ### Conclusions
	- ###### Observed from simulation
		- The average of sample statistic is close to the population parameter (accuracy)
		- The larger the sample size, the smaller the variance of the sample statistic (precision)
		- The number of repeated time doesn't change the results too much
		- The shape of the distribution of sample statistics could be symmetric and bell shaped
	- ###### Theoretical Results (CLT)
		- First version of CLT
		- CLT for the sample mean and proportion
		- True for any population distribution (the mean and variance need to exist)

- ### Versions of CLT
	- ###### iid samples, Sample sizes large
		- Random sample
		- Rule of Thumb
			- Mean Problem: At least $30$ observations
			- Proportion Problem: At least $15$ successes, at least $15$ failures
	- ###### One Sample
		- $\bar{X}\sim N(\mu,\frac{\sigma^2}{n})$
		- $\hat{p}\sim N(p,\frac{p(1-p)}{n})$
	- ###### Two Independent Samples
		- $\bar{X_{1}}-\bar{X_{2}}\sim N(\mu_{1}-\mu_{2},\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}})$
		- $\hat{p_{1}}-\hat{p_{2}}\sim N(p_{1}-p_{2},\frac{p_{1}(1-p_{1})}{n_{1}}+\frac{p_{2}(1-p_{2})}{n_{2}})$
