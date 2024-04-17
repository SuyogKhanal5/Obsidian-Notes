
- ### Confidence Interval (CI)
	- A observed interval derived
	- Repeated experiments again and again (many samples)
	- The frequency the intervals contain the true parameter
	- **Confidence level** - Percentage, e.g. $95$%
	- **Confidence Coefficient** - Decimal, e.g. $0.95$
	- Commonly used: $90$%, $95$%, $99$% confidence level
		- Default: $95$%

- ### Bootstrap CI (Percentile Method)
	- Starting from the bootstrap distribution, get the $2.5^{\text{th}}$ and $97.5^{\text{th}}$ percentile
		- `summarise(ci_lower=quantile(meanyear, 0.025),  ci_upper=quantile(meanyear, 0.975))`
	- Showing CI in histogram ![[Pasted image 20240413002305.png]]

- ### Bootstrap CI (Standard Error Method)
	- Starting from the *initial* sample
		- Get the center: $\bar{x}$
	- Starting from the *bootstrap* distribution
		- Get the *standard error*: $se$
	- CI: $\bar{x} \pm 1.96 * se$
	- Showing CI in histogram![[Pasted image 20240413002646.png]]

- ### CLT CI 
	- ###### Starting from the *initial* sample
		- Get the center $\bar{x}$
		- Get the *standard deviation*: $s$
	- CI: $\bar{x} \pm 1.96 \frac{s}{\sqrt{n}}$ (standard error $se=\frac{s}{\sqrt{n}}$)
	- Showing CI in histogram![[Pasted image 20240413003036.png]]

- ### Summary /  Comparison of CI
	- Three pairs of CI![[Pasted image 20240413003137.png]]
	- Will CI using CLT change if you rerun the program?
		- No
	- Will bootstrap CI change if you rerun the program?
		- Yes
	- ######  Advantage of bootstrap method
		- Parametric / Non-parametric method
		- Works for large or small sample size

- ### Infer Package
	- Simplifies much of our code![[Pasted image 20240416160241.png]]
	- ######  Steps:
		- 1. *specify* response variable
			- `specify(response= )`
		- 2. *generate* replicates
			- `generate(reps= , type= )`
		- 3. *calculate* summary statistics
			- `calculate(stat= )`
		- 4. *visualize* data (optional)
			- `visualize(data= , bins= ,)`
		- 5. get *CI*
			- `get_ci(x= , level= , type= , point_estimate= )`
			- Default level $=0.95$
			- `Visualize() + shade_ci(endpoints= , color= , fill= )`
		- You can use `%>%` in sequence until step 4 without creating a new data frame, but its better to make a new data frame after step 3 because  you need it in step 5 to get CI
	- Shade CI ![[Pasted image 20240416211931.png]]
	- Code Comparison![[Pasted image 20240416211955.png]]

- ### Are we sure about Confidence Level
	- ######  Does the interval indeed capture the true parameter with $95$% chance?
		- No idea for the penny example (as we don't know the population, hence the true mean value)
	- ###### Shovel example
		- $N=2400$ and $900$ red, $p=\frac{3}{8}$
		- This is a proportion problem
			- `specify(response=color, success="red")`
			- `calculate(stat="prop")`
		- CLT CI: $\bar{p} \pm 1.96 \sqrt{\frac{\bar{p}\bar{q}}{n}}$

- ### More about CI
	- ###### Interpreting CI
		- **Precise Interpretation**: If we repeated our sampling procedure a large number of times, we expect about $95$% of the resulting confidence intervals to capture the value of the population parameter
		- **Shorthand Interpretation**: We are $95$% confident that a $95$% confidence interval captures the value of the population parameter
	- ###### Other Confidence Level
		- Confidence level: $1-a$
		- Percentile method: Using percentile $\frac{a}{2}$, $1-\frac{a}{2}$
		- Standard error method and CLT: Replace $1.96$ by $z_\frac{a}{2}$
	- When the sample size is small, critical value from $t$ should be used for theoretical method, and the population should be approx. normal. 

