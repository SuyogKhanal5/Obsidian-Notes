
- ### Linear Model Assumptions (about the random error)
	- The mean of the probability distribution of $\epsilon$ is $0$
	- The variance of the probability distribution of $\epsilon$ is constant for all settings of the independent variable $x$, say the variance is $\sigma^2$
	- The probability of the distribution of $\epsilon$ is normal
	- The values of $\epsilon$ is normal
	- The values of $\epsilon$ associated with any two observed values of $y$ are are independent
	- **LINE** property
		- **L**: Linear pattern between $y$ and $x$
		- **I**: Independent
		- **N**: Normal Distribution
		- **E**: Equal Variance
	- Normal distribution
		- Multiple points with $x=x_0$
			- $E(y|x=x_{0})= E(\beta_{0}+\beta_{1}x_{0} + \epsilon) = \beta_{0}+ \beta_{1}x_0$
			- $V(y|x=x_{0})= V(\beta_{0}+\beta_{1}x_{0} + \epsilon) = \sigma^2$ ![[Pasted image 20230926122735.png|500]]
	- Independency

- ### Linear Pattern / Mean 0
	- Sum of residuals will always be $0$
		- This is the condition when solving $\beta$s
	- Non-linear pattern
	- Sum of residuals at different intervals![[Pasted image 20230926122915.png|500]]

- ### Equal / Constant Variance
	- Homoscedasticity vs. Heteroscedasticity ![[Pasted image 20230926123156.png|500]]

- ### Normal Distribution
	- Histogram and QQ plot ![[Pasted image 20230926123253.png|500]]

- ### Outliers
	- Scatterplot, histogram, boxplot ![[Pasted image 20230926123411.png|500]]

- ### Independent
	- Understand your data
	- Be careful in time series data ![[Pasted image 20230926124024.png|500]] ![[Pasted image 20230926124125.png|500]]

 - ### More about Regression
	 - What if residual plots are not satisfied
		 - Remove outliers
		 - Transformation
		 - Non-linear model
		 - Weighted Regression
		 - Time series model
		 - …
	- More about least square method
		- "best" in what sense
	- More about regression
		- Ridge Regression
		- Lasso Regression
		- …

- ### Francis Galton
	- A polymath
	- Research late 19th century
	- Statistical methods for analyzing heritable traits, especially in humans
		- Quetelet: First fitted normal distribution to human data (chest measurements)
		- Galton: Was this distribution heritable?
	- Sweet Peas
		- First regression line
	- Parent height vs Child height

- ### Sweet Peas
	- Packets of sweet peas of 7 different sizes
		- 15-21 (0.01 inch)
	- The sizes of their offspring were measured ![[Pasted image 20230926124922.png|500]]
		- 100 offspring from each size
		- Many with same size 
	- Mean diameter of child seeds vs mean of parents
		- `weighted.mean` function
		- ```meanpeas <- peas %>% group_by(parent) %>%  
		summarise(meanoffspring=weighted.mean(offspring, frequency))```
	- Mean in each parent group ![[Pasted image 20230926125416.png|500]]
	- Mean and SD of $x$ and $y$ ![[Pasted image 20230926125445.png|500]]

- ### First Regression Line
	- Seed sizes distributed normally
	- The progeny grown from small seeds produced plants with seeds closer to the mean of the distribution
	- "Reversion to the mean" ($R$ in the graph is for slope) ![[Pasted image 20230926125630.png|500]]

- ### Regression to the Mean
	- Further illustrated through Galton's height data
		- An adult child is closer to average height than its parents
		- Parents are closer to average height than their child
	- Regression to the mean
		- If a variable is extreme on its first measurement, it will tend to have been closer to the average on its second measurement
		- If it is extreme on its second measurement, it will tend to have been closer to the average on its first

- ### Galton's Height Example
	- Data contains
		- About 1000 adult children
		- A family could have multiple children in the data
			- Father's height, mother's height, adult (child) gender, child's height
	- Does gender matter for height? 
		- Female child's height multiplied by $1.08$
	- Mother's height or Father's height?
		- Midpoint of parents’ heights (mother’s height multiplied by $1.08$ as well)
	- Regression of child height ~ mid-height of parent 
		- Definition for the new x and y variable