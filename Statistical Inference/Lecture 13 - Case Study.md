
- ### New Dataset: Seattle House Prices
	- From `moderndive` package
	- Sale prices of homes sold between May 2014 and May 2015 in King County, WA
	- $21,613$ houses and $21$ variables  
	- Dependent variable: `price`  
	- Try to find what can help explain the house prices  
	- Multiple regression model

- ### Seattle House Prices Independent Variables
	- ###### Discrete
		- `floors`  
		- `waterfront`  
		- `view`  
		- `condition`  
		- `grade`  
		- `zipcode`
	- ###### Continuous
		- `bedrooms`  
		- `bathrooms`  
		- `sqft_living`  
		- `sqft_lot`  
		- `yr_built`  
		- `yr_renovated`

- ### Distribution of Price and Size
	- Symmetric or Skewed?![[Pasted image 20231024115523.png]]
	- Transformation needed?![[Pasted image 20231024115559.png]]

- ### Log Transformation
	- For *right skewed* data![[Pasted image 20231024115644.png]]

- ### Discrete X Variables
	- Distributions![[Pasted image 20231024115858.png]]
	- ###### Are they useful?
		- `waterfront` - Possibly, $\frac{163}{21613} < 1\%$ waterfront houses
		- `condition` - Possibly, levels $1$ and $2$ may be combined
		- `floors` - Possibly, might be better to have $2$ levels ($1.0$ or not)
		- `grade` - Overall grade given to housing unit, useful
		- `zipcode` - Specific zip codes make more expensive houses

- ### Continuous X Variables
	- `lnprice` vs. `lnsize`![[Pasted image 20231024120555.png]]
	- `yr_built` - Year built
		- Average $\ln(\text{house price})$ by year![[Pasted image 20231024120757.png]]
	- `bedrooms` - Number of bedrooms
		- Average $\ln(\text{house price})$ by bedrooms![[Pasted image 20231024120911.png]]
	- `bathrooms` - Number of bathrooms
		- Average $\ln(\text{house price})$ by bathrooms![[Pasted image 20231024121030.png]]
	- `sqft_lot` - Lot size
		- Correlations between sqft of house and the lot? $0.17$, not high
		- Distribution ![[Pasted image 20231024121130.png]]
		- Summary statistic![[Pasted image 20231024121147.png]]

- ### Influential Points of Erroneous Records?![[Pasted image 20231024121340.png]]
- ### Before Regression
	- ###### Suspicious observations  
		- $7.5$ bathrooms, price $450,000$ – live with it  
		- $33$ bedrooms, price $640,000$ – either delete it, or correct the data: for example, bedrooms = $3$ (instead of $33$) 
	- ###### Potential discrete variables  
		- `waterfront` – $2$ levels  
		- `condition` – $4$ levels $(1\land2, 3, 4, 5)$
		- `floors` – $2$ levels ($1$ or not)  
		- `expzip` – $2$ levels (in the most expensive $10$ zip codes or not)  
		- `largelot` – $2$ levels (lot size $> 43560$ sqft, or $1$ acre)  
	- ###### Potential continuous variables  
		- `yr_built`, `bedrooms` – both first and second order  
		- `lnsize`, `bathrooms` – first order only  
	- Could have interactions

- ### Boxplots ![[Pasted image 20231024122115.png]]
- ### Scatterplots ![[Pasted image 20231024122129.png]]
- ### First Regression: Model 1
	- Put all variables in, discrete and continuous (`yr_built` and `bedrooms` also have second order terms)![[Pasted image 20231024122205.png]]

- ### Interaction Model: Model 2
	- Can have all different interactions: Show interaction of `lnsize` and all discrete as an example![[Pasted image 20231024122343.png]]
	- ###### Revise the model:
		- Delete the interaction of `lnsize` and `largelot`
		- `condition` level - $2$ levels ($5$ or not)![[Pasted image 20231024122507.png]]

- ### Model 1 or Model 2?
	- F statistic for overall model (be careful when df are different)  
	- Adjusted $R^2$ (higher), RMSE (lower)  
	- AIC, BIC (lower)![[Pasted image 20231024122554.png]]
	- ###### Residual Plots![[Pasted image 20231024122623.png]]
	- ###### Making Estimation for Prediction
		- Must input the value for the variables included in the model  
			- For example, need to input `yr_built2` etc.  
			- No need to put in the interaction
			- `lnprice_pred <- predict(model4,  newdata=data.frame(lnsize=log(5000), yr_built=2000,  yr_built2=2000^2, ...)`
		- As $y$ is also transformed, the house price needs to take exponent
			- `exp(ln_pricepred)`
		- Predictions:![[Pasted image 20231024122822.png]]