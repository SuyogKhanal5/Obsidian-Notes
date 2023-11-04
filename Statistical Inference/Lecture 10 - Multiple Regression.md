
- ### General Multiple Regression Model
	- ###### General Regression Model
		- $y=\beta_0 + \beta_1x_1 + \dots + \beta_kx_k + \epsilon$
		- Linear Component: $E(y|x)=\beta_0 + \beta_1x_1 + \dots + \beta_kx_k$
		- Independent Variable: $y$
		- Dependent Variable: $x_1, x_2 \dots x_k$
			- Could be combinations of linear terms, higher order terms and categorical terms
		- Random Error: $\epsilon$
	- Method: Minimize SSE

- ### Multiple Regression Model Assumptions (About Random Error)
	- The mean of the probability distribution of $\epsilon$ is $0$
		- Deterministic Component: $E(y|x)=\beta_0+\beta_1x_1+L\beta_kx_k$
	- The variance of the probability distribution of $\epsilon$ is constant for all settings of the independent variable $x$, say the variance is $\sigma^2$
	- The probability distribution of $\epsilon$ is normal
	- The values of $\epsilon$ observed with any two values of $y$ are independent
	- *Summary*: Same as linear regression

- ### Teaching Score Evaluation
	- Previously, we had run regressions on beauty score and gender
		- Beauty Score: $R^2=0.035$, significant model
		- Gender: $R^2=0.017$, significant model
	- Can we improve the model in explaining $y$ variation by using both beauty score and gender?

- ### Model with Continuous and Dummy Variable I: Parallel Slopes
	- Regression with only one dummy variable and one continuous 
	- ###### Model: `teachingScore~beautyScore and Gender`
		- Beauty Score: $x_1$, Gender: $\begin{equation*} x_2 = \begin{cases} 0 \text{ if female} \\ 1\text{ if male} \end{cases}\end{equation*}$
		- What is the case for male and female?
			- Female: When $x_2 = 0, E(y)=\beta_0+\beta_1\cdot x_1+\beta_2\cdot0=\beta_0+\beta_1x_1$
			- Male: When $x_2 = 1, E(y)=\beta_0+\beta_1\cdot x_1+\beta_2\cdot1=(\beta_0+\beta_2)+\beta_1x_1$
		- What do the $\beta$s mean?
			- $\beta_1$: The expected increase in teaching score, when beauty score is increased by 1, *given that female or male are forced to have the same effect*
			- $\beta_0$: The expected teaching score when beauty score is $0$ for *female*
			- $\beta_1$: The expected teaching score when beauty score is $0$ for *male*
			- $\beta_2$: The difference in mean teaching score for males and females when beauty score is $0$
	- ###### Output:![[Pasted image 20231010125030.png]]

- ### Parallel Slope: Discussion
	- The slope for female and male are the same, positive, significant
		- There is associated *effect* of beauty score on teaching score
		- The effect of beauty score on teaching score is the *same* for male and female
	- This may not be true as you forced a parallel model

- ### Model with Continuous & Dummy Variable II: Separate Slopes
	- Regression with only one dummy variable and one continuous and interaction
	- ###### Model: `teachingScore~beautyScore and Gender`
		- Beauty Score: $x_1$, Gender: $\begin{equation*} x_2 = \begin{cases} 0 \text{ if female} \\ 1\text{ if male} \end{cases}\end{equation*}$
		- Model: $E(y)=\beta_0+\beta_1x_1+\beta_2x_2 + \beta_3x_1x_2$
		- What is the case for male and female?
			- Female: When $x_2 = 0, E(y)=\beta_0+\beta_1\cdot x_1+\beta_2\cdot0+\beta_3\cdot x_1\cdot 0=\beta_0+\beta_1x_1$
			- Male: When $x_2 = 0$, $E(y)=\beta_0+\beta_1\cdot x_1+\beta_2\cdot0+\beta_3\cdot x_1\cdot 1$ 
			  $=(\beta_0+\beta_2)+(\beta_1 + \beta_3)x_1$
			- $\beta_1$: The expected increase in teaching score, when beauty score is increased by 1 for *female*
			- $\beta_1 +\beta_3$: The expected increase in teaching score, when beauty score is increased by 1 for *male*
			- $\beta_0$: The expected teaching score when beauty score is $0$ for *female*
			- $\beta_0 + \beta_2$: The expected teaching score when beauty score is $0$ for *male*
		- Same case as separated regressions on gender 
	- ###### Output: ![[Pasted image 20231010130237.png]]

- ### Separate Slopes Discussion
	- ###### Called **Interaction Model**
		- Both slopes are positive: Higher the beauty score, the higher the teaching score
		- Slope for beauty score for male is *more* positive $(p$-value$=0.015$, significant$)$ 
		- The effect of beauty score on teaching score depends on the value of gender
	- ###### Main effect and interaction
		- Main effect from beauty score, main effect from gender
		- When considered together, there is additional effect interaction
	- ###### When should you run separate simple regressions for male and female respectively or run a parallel model?
		- Find out if the difference between the slopes is significant or not
		- Run interaction model
			- Interaction term *is significant*
				- Keep main effects even if main effects may not be significant
			- Interaction term is ***not significant***
				- There is no significant difference between the slopes
				- If you run simple regressions separately, will the two slopes be the same?