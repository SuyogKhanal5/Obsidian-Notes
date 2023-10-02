
- ### Rethink Life Expectancy Model
	- Regression of life expectancy ~ $\log$(GDP) $\Leftrightarrow$ $y=$ life expectancy, $x'=\log$(GDP) `lm(y~x')`
	- ###### Intrinsically linear model
		- Model: $y'=\beta_{0}+\beta_{1}x'+\epsilon$
		- Estimation for $\beta$s: Based on Sum of Squares after transformation (least square method)
		- Example:
			- $\ln(y)=\beta_{0}+\beta_{1}x+\epsilon$
			- $y=\beta_{0}+ \beta_{1}\ln(x)+\epsilon$
			- $y=\beta_{0}+\beta_{1}\frac{1}{x}+\epsilon$

- ### Binary Response
	- ###### Response variable $Y$: Binary variable (success/failure)
		- Expectation of $Y$: Probability of success $p(x)$
		- $Y=1$: Success, outcome of interest
	- Logit function: logit$(p)=\ln(\frac{p}{1-p})$ ![[Pasted image 20230929122821.png|500]]
		- Domain: ($0,1$)
		- Range: ($-\infty,\infty$)

- ### Why not Linear Regression?
	- ###### What if a regular regression?
		- $Y=\beta_{0}+\beta_{1}x_{1}+\beta_{2}x_{2}+\dots+\beta_{k}x_{k}+\epsilon$
	- ###### Binary variable 
		- Expectation of $Y$: Probability of success, $E(Y)=p$
		- Take expectation on each side
			- Left side: $p$, range in $[0,1]$
			- Right side: $\beta_{0}+\beta_{1}x_{1}+beta_{2}x_{2}+\dots+\beta_{k}x_{k}$ not necessarily in $[0,1]$
	- ###### Multiple Categories
		- $\begin{equation*} Y = \begin{cases} 1 \text{ if stroke} \\ 2\text{ if drug overdose} \\ 3 \text{ if epileptic seizure} \end{cases}\end{equation*}$
		- Ordering in 3 levels matters
		- The difference between stroke and drug overdose is the same as the difference between drug overdose and epileptic seizure
		- Is this the case?
	- What do we want to estimate?
		- The *probabilities* of falling in the categories

- ### Logistic Regression
	- ###### Fit logit of probability as linear function of $x$
		- $\ln(\frac{p(x)}{1-p(x)})=\beta_{0}+\beta_{1}x$
		- $\frac{p(x)}{1-p(x)}=e^{\beta_{0}+\beta_{1}x}$
		- $p(x)=\frac{e^{\beta_{0}+\beta_{1}x}}{1+e^{\beta_{0}+\beta_{1}x}}$
	- Logit linear model
	- ###### How to estimate $\beta_{0}$ and $\beta_{1}$
		- Maximum likelihood technique, not least square method
		- Rely on statistical software (R)

- ### Data: Space Shuttle Launches
	- Incidence of failure of O-rings in space shuttle launches vs. launch temperature (prior to the Challenger disaster of 1986)
	- Comparative stem and leaf plot ![[Pasted image 20230929125532.png|500]]
	- Input data
		- Response $=1$ means success
	- Code
		- `temp<-c(58,57,53,63,75,70,70,66,67,67,67,...,81)` 
		- `fail<-c(rep(1,7),rep(0,16))`
		- `launch <- data.frame(fail,temp)`

- ### Fit Regression
	- Fit regression
		- `launch_model<-glm(data=launch, fail~temp, family=binomial)`
	- GLM is used instead of LM for General Linear Model

- ### Odds and Odds Ratio
	- ###### Odds of Outcome: $\frac{p(x)}{1-p(x)}$
		- Odds $=2$? A success is twice as likely as a failure
		- Odds $=\frac{1}{2}$? A success is half as likely as a failure
	- ###### Odds Ratio (OR): $\frac{p(x+1)/(1-p(x+1)}{p(x)/(1-p(x))}$
		- Change of odds when $x$ increases by 1 unit
		- OR $= 1$: Increase in $x$ doesn't affect odds of success
		- OR $> 1$: Increase in $x$ results in higher odds of success
		- OR $< 1$: Increase in $x$ results in lower odds of success

- ### Odds Ratio In Logistic Regression
	- Mathematically calculated with $e^{\text{slope}}$
	- In R with package `epiDisplay`
		- `logistic.display(launch_model)` ![[Pasted image 20230929130747.png|500]]
	- For each additional degree of temperature, the odds of failure will decrease by a factor of 0.79 (21%)  

- ### Fitted Values
	- Fitted values:
		- Probability of success
		- `launch_model$fitted.values`
	- Fitted Value Plot![[Pasted image 20230929130951.png|500]]
- ### Classification
	- How to classify success?
		- At threshold $0.5$
		- At threshold $\hat{p}=\frac{16}{23}$
	- Equivalently, what is the cutoff for temperature such that if the launching temperature is larger than the cutoff, it will be predicted as failure? ![[Pasted image 20230929131222.png|5--]]

- ### Challenger Disaster
	- What happened to space shuttle Challenger?  
	- Occurred 1/28/1986  
	- Broke apart 73 seconds into its flight  
	- Failure of O-ring seals  
	- Launch temperature: 31F  
	- Predicted probability of launch failure using above model
	- `> predict(launch_model, newdata=data.frame(temp=31), type="response")`
	- $99.96088$%, almost a for sure failure

- ### Model Diagnostics and Evaluation
	- Likelihood ratio test  
	- Hosmer-Lemeshow test  
	- Wald test  
	- Pseudo $R^2$  
	- ROC curve  
	- Cross validation