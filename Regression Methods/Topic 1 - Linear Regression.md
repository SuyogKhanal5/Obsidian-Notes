
- ### Least Squares Estimator
	- $\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i$
	- $\bar{y}=\frac{1}{n}\sum_{i=1}^{n}y_i$
	- $s_{xx}=s^2_x=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2$
	- $s_{yy}=s^2_y=\frac{1}{n-1}\sum_{i=1}^{n}(y_i-\bar{y})^2$
	- $s_{xy}=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})$
	- $r=\frac{s_{xy}}{\sqrt{s_{xx}s_{yy}}}=\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum_{i=1}^{n}(x_i-\bar{x})^2}\sqrt{\sum_{i=1}^{n}(y_i-\bar{y})^2}}$
	- ###### Least Squares Estimator
		- $({\hat{\beta}_0},{\hat{\beta}_1)}=\text{arg min}_{b_0,b_1}\sum_{i=1}^{n}(y_i-b_0-b_1x_1)^2$
		- $\hat{\beta}_1=\frac{s_{xy}}{s_{xx}}=r \cdot \frac{s_y}{s_x}$
		- $\hat{\beta}_0=\hat{y}$-$\hat{\beta}_1\hat{x}$
		- Estimated regression line is $\hat{Y}=$ $\hat{\beta}_{0}-\hat{\beta}_1\hat{x}$
		- For $i^\text{th}$ unit $x_i$ the fitted/predicted value is $\hat{y_i}=\hat{\beta}_{0}-\hat{\beta}_1\hat{x}i$
		- $\hat\epsilon_{i}=y_i-\hat{y_i}$ is the residual

- ### Residuals
	- Residual vector $\mathbf{\hat{\epsilon}}$ (in bold) or sometimes used in these notes as $\vec{\epsilon}$ is the vector of all the residuals
	- The residual vector sums to 0
	- The residual vector has the following properties
		- $\sum_{i=1}^{n}\hat{\epsilon_{i}}=0$
		- $\sum_{i=1}^{n}x_i\hat{\epsilon_{i}}=0$
	- Let $\vec{x}=(x_1,x_2,\dots,x_n)'$ and $a=(1,1,\dots,1) \in \mathbb{R}^n$
		- $\langle \vec{a},\vec{\epsilon}\rangle :=\sum_{i=1}^{n}\hat{\epsilon_{i}}=0$. It follows that $\frac{1}{n}\sum_{i=1}^{n}y_i=\bar{y}$
		- $\langle \vec{x},\vec{\epsilon}\rangle := \sum_{i=1}^{n}\hat{x_i\epsilon_{i}}=0$
	- The residual vector is orthogonal to both $\vec{a}$ and $\vec{x}$
	- The vector of observed response variables is $y=(y_1,y_2,\dots,y_n)'$
	- The vector of fitted values is $\hat y= (\hat y_1,\hat{y_2},\dots,\hat{y_n})'$
	- Residual vector is the difference of these values: $\vec{\epsilon}=y-\hat{y}$
	- The equivalent forms of the regression line motivates us to consider "deviations" from the average, for both predictors and responses
		- Let $\widetilde{x}=x-\bar{x}\cdot 1$ and $\widetilde{y}=y-\bar{y}\cdot 1$
	- The deviation from the average vectors satisfy $\widetilde{y}=\hat{\beta_1}\widetilde{x}+\vec{\epsilon}$
		- $\hat{\beta_1}\widetilde{x}$ is the projection $\widetilde{y}$ onto the vector $\widetilde{x}$
		- $\langle \vec{x},\vec{\epsilon}\rangle=0$, i.e $\vec{x}\perp \vec{\epsilon}$
		- $\vec{\epsilon}=y-\hat{y}=\widetilde{y}-\hat{\beta_1}\widetilde{x}$

- ### Sum of Squares and ANOVA
	- Sum of squares corresponding to the simple linear regression
		- Total sum of squares
			- SST $= \sum_{i=1}^{n}(y_i-\bar{y})^2$
		- Regression sum of squares
			- SSR $= \sum_{i=1}^{n}(\hat y_i-\bar{y})^2$
		- Residual sum of squares
			- SSE $= \sum_{i=1}^{n}(y_i-\hat{y})^2=\sum_{i=1}^{n}(\hat{\epsilon_i}-\bar{\vec{\epsilon}})^2$
	- It holds that SST = SSR + SSE

- ### Coefficient of Determination
	- Coefficient of determination, $R^2$ is defined as:
		- $R^2=\frac{\text{SSR}}{\text{SST}}=1-\frac{\text{SSE}}{\text{SST}}$
	- $R^2$ is the proportion of the variation explained by the regression line
	- $R^2$ is a scale invariant measure of how close the regression line is to all the data points
	- Properties of $R^2$\
		- $0\le R^{2}\le 1$
		- $R^2=1$ means all points exactly on the line
		- $R^2=0 \Rightarrow\hat{\beta_1}=0$, no linear relationship between response and predictor, i.e $\widetilde{y} \perp \widetilde{x}$
	- There might be a non linear relationship, which $R^2$ does not capture

- ### Variance Estimation
	- $\sigma^2$ is the variance of the $\epsilon_i$'s
	- Use the sample variance of $\hat{\epsilon}_i$'s
	- Adjust the degrees of freedom by two, since we have estimated $\beta_0$ and $\beta_1$ already
	- Estimate $\sigma^2$ with Mean Squared Error (MSE)
		- $s^2_e=\frac{1}{n-2}\sum_{i=1}^n\hat{\epsilon}_i^2$
	- $s_e$ is called Root Mean Squared Error (RMSE)
	- By dividing by $n-2$, we get an unbiased estimator (this is the adjustment for degrees of freedom)
	- Equivalent formula:
		- $s^2_e=s^2_y\cdot(1-r^2)\cdot\frac{n-1}{n-2}$

- ### Properties of LSE
	- $\hat{\beta_0},\hat{\beta_1},s_e^2$ are unbiased and random
		- Random because if you repeat the same experiments or draw a different sample you get different values because errors in $\vec{\epsilon}$ are random
		- Anything with $\epsilon$ or $y$ is a random variable
	- $\hat{\beta_0}$ and $\hat \beta_1$ have the normal distribution
		- $\hat{\beta_{0}} \sim N[\beta_{0},\text{Var}(\hat{\beta_0})]$, $\text{Var}(\hat{\beta_0})]=\frac{\sigma^2}{n}+\frac{\sigma^2\cdot\bar{x}^2}{\sum_{i=1}^n(x_i-\bar{x})^2}$
		- $\hat{\beta_{1}} \sim N[\beta_{1},\text{Var}(\hat{\beta_1})]$, $\text{Var}(\hat{\beta_1})]=\frac{\sigma^2}{\sum_{i=1}^n(x_i-\bar{x})^2}$
	- $\frac{(n-2)s^2_e}{\sigma^2}\sim X^2_{n-2}$

- ### Standard Errors of the LSE and t-distribution
	- The standard deviation of $\hat{\beta_1}$ is given by:
		- $\text{sd}(\hat \beta_1)=\sqrt{\frac{\sigma^2}{\sum_{i=1}^n(x_i-\bar{x})^2}}=\frac{\sigma^2}{(n-1)s^2_x}=\frac{\sigma}{\sqrt{n-1}\cdot s_x}$
	- However the noise variance $\sigma^2$ is unknown so we estimate $\text{sd}(\hat \beta_1)$ by plugging in $s^2_e$ for $\sigma^2$ and we call this estimate the standard error
		- $\text{se}(\hat \beta_1)=\frac{s_e}{\sqrt{n-1}\cdot s_x}$
	- It turns out that:
		- $\frac{\hat{\beta_1}-\beta_1}{\text{se}(\hat \beta_1)}\sim t_{n-2}$


