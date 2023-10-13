- ### Exploratory Data Analysis
	- We did teaching score vs beauty score and teaching score vs age before
	- Age is continuous, represented as an integer in the data
	- Will the relationship between teaching score and beauty score be similar within each age category?
		- Take a subset with age in (47, 52, 57) 
	- Smooth Line Separately vs Smooth Line with Same Slope ![[Pasted image 20231013123250.png]]

- ### Model with Two Continuous Variables I: No Interaction Terms
	- Regression with two continuous
		- It is normally the case that the regressors are independent
	- ###### Model: `teachingScore~beautyScore and Age`
		- Correlation Matrix![[Pasted image 20231013123510.png]]
		- Model: $E(y) = \beta_{0} +\beta_{1}x_{1}+\beta_{2}x_2$
		- Beauty Score: $x_1$, Age: $x_2$
		- What do the $\beta$s mean?
			- $\beta_0$: The expected teaching score when beauty score is $0$ and age is $0$
			- $\beta_1$: The expected increase in teaching score, when beauty score is increased by $1$, *while age is held fixed*
			- $\beta_2$: The increase in teaching score when age is increased by $1$ and *beauty score is held fixed*
	- ###### Outputs ![[Pasted image 20231013124513.png]]

- ### No Interaction: Discussion
	- ###### The slope for beauty score is significant
		- There is associated *positive effect* of beauty score on teaching score
		- The effect of beauty score on teaching score is *the same* for all ages
		- This may not be the true case as you forced same slope
	- ###### The slope for the beauty score is insignificant
		- It was insignificant in simple regression

- ### Regression Plane
	- In 3D the best fit is a plane
	- `plotPlane()` function from `rockchalk` package
	- `plotPlane(model1, plotx1="bty_avg", plotx2="age")`![[Pasted image 20231013124912.png]]

- ### Contour Plot
	- Representing a 3D surface by plotting constant $z$ slices
	- `contour()` function in `rsm` package
	- `rsm(model1, bty_avg~age)` ![[Pasted image 20231013125136.png]]

- ### Model with Two Continuous Variables II: Interaction Model
	- Regression with two continuous and interaction
		- It is normally the case that the regressors are independent
	- ###### Model: `teachingScore~beautyScore and Age`
		- Model: $E(y) = \beta_{0} +\beta_{1}x_{1}+\beta_{2}x_{2}+\beta_{3}x_{1}x_{2}$
		- Beauty Score: $x_1$, Age: $x_2$
		- What do the $\beta$s mean?
			- $\beta_0$: The expected teaching score when beauty score is $0$ and age is $0$
			- $\beta_{1}+ \beta_{3}x_{2}$: The expected increase in teaching score, when beauty score is increased by $1$, *while age is held fixed*
			- $\beta_{2}+ \beta_{3}x_{1}$: The increase in teaching score when age is increased by $1$ and *beauty score is held fixed*
	- ###### Output: ![[Pasted image 20231013130251.png]]

- ### Interaction Model: Discussion
	- ###### Beauty Score 
		- Mainly has positive effect on teaching score
		- $385$ observations with age $\ge 37.6$ $(83\%)$
		- The slope for beauty score is *more positive* when age is older
		- The effect of beauty score on teaching score depends on the value of age
	- ###### Age
		- Mainly has a negative affect on teaching score
		- $333$ observations with beauty score $\le$ 5.2 $(69\%)$
		- The slope for age is *more negative* when beauty score is lower
		- The effect of age on teaching score depends on the value of beauty score
	- Beauty Score and Age are "interacting" with each other
	- ###### Main effect and interaction
		- Main effect from beauty score, main effect from age
		- When considered together, there is additional effect: **Interaction**
		- When interaction is significant, include the main effects anyway even if some may not be significant

- ### Regression Plane and Contour Plot
	- Regression Plane is twisted when there is interaction term
	- Contour plot has non-parallel lines![[Pasted image 20231013131106.png]]