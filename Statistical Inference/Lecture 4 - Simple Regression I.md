
- ### Scatterplots
	- Looking at the points on a scatterplot, we can see if the variables have a linear relationship
	- ![[Pasted image 20230915121802.png|500]]
	- We can model the relationship between $x$ and $y$
		- Dependent Variable ($y$): Also called response
		- Independent Variable ($x$): Also called predictor or explanatory variable

- ### Coefficient of Correlation
	- **Covariance**: Measures how much TWO random variables change together
	- ###### Pearson Correlation Coefficient $r$
		- Normalized version of covariance
			- Independent of the units in which $x$ and $y$ are measured
		- Measures the strength of a *linear* relationship
		- $|r| \le 1$
	- ###### Correlation: Doesn't mean causal relationship
		- Just means that they are correlated
		- They may both both be correlated with a hidden variable
	- ###### Low Correlation: Doesn't mean $x$ and $y$ are unrelated
		- Just means that they are not *linearly* related
		- There may exist a non-linear relationship, like quadratic, exponential, etc. 
	- ![[Pasted image 20230915122336.png|500]]
	- We classify $r$ as follows:
		- Weak: $|r| \le 0.5$
		- Moderate: $0.5 < |r| < 0.8$
		- Strong: $|r| \ge 0.8$

- ### Types of Modeling
	- ###### Modeling for **explanation**
		- Determine the significance of relationships
		- Identify factors that have impact on response
		- Quantify the relationship
		- Simple but useful approach: regression
			- Simple regression
			- Multiple regression
	- ###### Modeling for **prediction**
		- Don't care how all of the variables work and how to explain the relationship
		- Make good prediction about the response
		- Other methods in machine learning

- ### A Little Theory
	- Linear Model: $y = \beta_{0}+ \beta_{1} + \epsilon$
	- Error of Prediction: $\epsilon = y - (\beta_{0}+\beta_1x)$
	- Sum of Squares of Error (SSE): SSE = $\sum (y_{i}- (\beta_{0}+\beta_1x_i))^2$
	- How to find $\beta_{0}$ and $\beta_1$
		- Find them such that SSE is minimized
	- How to minimize SSE?
		- Use partial derivatives
	- (Ordinary) Least Square Line (OLS)
	- Regression Line: $\hat{y} = \hat{\beta_{0}}+ \hat{\beta_{1}}x$
	- Residual: $\epsilon_{i}= y_{i}- \hat{y_i}$
	- Other method: e.g. Minimize the sum of absolute error
	- ![[Pasted image 20230915123809.png|500]]

- ### Step 1: Exploratory Data Analysis
	- ###### Look at the raw data
		- Look at variables and observations
		- Check for missing values
		- See if there are any erroneous records or outliers
	- Summary statistics
	- ###### Try Visualization
		- Univariate: Histogram
		- ![[Pasted image 20230915124833.png|500]]
		- Bivariate: Scatterplot
		- ![[Pasted image 20230915124854.png|500]]
	- Check the correlation matrix
	- ![[Pasted image 20230915124745.png|500]]

- ### Step 2: Fit Regression
	- We want to see what explanatory variable ($x$) can explain the $y$ variable
	- ###### ```lm()``` function
		- ```modelname <- lm(y~x, data=dataframe_name```
		- Regression model is saved in ```modelname```
	- ###### Details of the regression
		- ```get_regression_function```
		- Regression table with estimated $y$-intercept and slope: ```get_regression_table()```
		- Fitted values and residuals: ```get_regression_points()```
		- Model diagnostics: ```get_regression_summaries()```

- ### Regression Table Example
	- ###### Estimates
		- $\hat{\beta_{0}}$: Intercept
		- $\hat{\beta_{1}}$: ```bty_avg``` (regressor name)
	- ###### Regression Model
		- $y = 3.880 + 0.067x + \epsilon$
		- $\hat{y} = 3.880 + 0.067x$
	- ###### Meaning of $\hat{\beta_{0}} = 3.880$
		- This is the *expected* teaching score when beauty is $0$
		- Not meaningful for a lot of cases
	- ###### Meaning of $\hat{\beta_{1}} = 0.067$
		- This is the *expected* increase in teaching score when beauty score increases by one unit
	- We are basically creating a line of best fit 
	- Statistically Significant - Cannot be observed by random chance, pattern is always there
	- ###### Is your regressor useful in explaining/predicting the dependent variable?
		- Check the **p-value** for the regressor
			- What is the $p$-value?
				- It is for hypothesis testing $H_{0}: \beta_{1}= 0$ vs $H_{a}: \beta_{1}\ne 0$
			- Statistically Significant: $p$-value $< 0.05$
			- Marginally Significant: $0.05 < p$-value $< 0.1$ 
			- Could be more generous when making predictions
		- ```std_error``` and ```statistic``` are both for this hypothesis testing
		- No need to check $p$-value for the intercept
	- ```lower_ci``` and ```upper_ci```
		- These are for confidence intervals of $\beta$
		- ![[Pasted image 20230915131534.png|500]]

- ### Fitted Values
	- Same $x$ values have same fitted values, but different residuals
		- ```Score_hat = beta0_hat + beta1_hat * bty_avg```
		- `Residual = score – score_hat`
		- `bty_avg = 5, score_hat = 3.880 + 0.067 * 5 = 4.215 ` 
		- `Score = 4.7, residual = 4.7 - 4.215 = 0.485`  
		- `Score = 4.1, residual = 4.1 - 4.215 = -0.115`

- ### Show Regression Line
	- `ggplot()+ geom_point() + labs() +  geom_smooth(method="lm",se=FALSE)`
	- ![[Pasted image 20230915132004.png|500]]

- ### Residual Plots
	- What are we looking for? - Randomness
		- Symmetric bell-shaped curve
		- No obvious outliers
		- No cone shape
	- ![[Pasted image 20230915132105.png|500]]

- ### What happens using `cls_students` as the regressor?
	- Residual Plots
	- Violations?
	- ![[Pasted image 20230915132316.png|500]]

- ### What is SSE under Regression?
	- ###### `mutate()` in R
		- Add new variables and preserve existing ones
	- ###### Try different SSEs and compare
		- Significant model using `bty_avg`
			- `points1 %>% mutate(squared_residuals = residual^2) %>%  
			  `summarize(sse1 = sum(squared_residuals)) 
			- `evals %>% mutate(anyres_sq = (score - (5 + 0.1 * bty_avg ))^2) %>% 
			  `summarize (sse2=sum(anyres_sq))  
			- `evals %>% mutate(anyres_sq = (score - (5 - 0.1 * bty_avg ))^2) %>% 
			  `summarize (sse2=sum(anyres_sq))
		  - Insignificant model using `cls_students`
			  - `points3 %>% mutate(squared_residuals = residual^2) %>%  
			    `summarize(sse3 = sum(squared_residuals))  
			- `evals %>% mutate(anyres_sq = (score - (5 - 0.1 * cls_students ))^2) %>% summarize (sse2=sum(anyres_sq)) 
			- `evals %>% mutate(anyres_sq = (score - (5 - 0.1 * cls_students ))^2) %>% summarize (sse2=sum(anyres_sq))`

- ### Model Diagnostics
	- Model Summaries
	- ![[Pasted image 20230915132436.png|500]]
	- ###### R-Squared $R^2$
		- $3.5$% of the *total* sample variation in $y$ (teaching score) can be explained by using $x$ (beauty score) to predict $y$ in the straight *line model*
		- In simple regression, this is correction$^2$
			- `Corr(score, bty_avg)=0.187, 0.187^2=0.035`
	- The higher the $R^2$ the more successful the model is explaining $y$ variation
	- ###### Adjusted $R^2$
		- Taking into account the number of regressors
		- Similar explanation as $R^2$
		- Generally smaller than $R^2$
	