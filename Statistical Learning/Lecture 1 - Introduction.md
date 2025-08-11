
- ### What is type 3 error?
	- Answering the wrong question, most costly
	- Issue is usually building a very precise model, but based on the wrong question
	- Ex. Challenger space shuttle, launch or not to launch? (launching at below freezing temperature)
		- Rocket failed at higher temperature, rocket was below dangerous temperature, but launched and temperature was too low, caused new error
		- Original question: Of those with blow bys, what is the temperature dependence?
		- Better question: What is the temperature dependence of existence of blow bys?

- ### Accelerated Failure Time
	- Accelerated failure time says that time literally scales between conditions $t_{\text{condition2}}=a \times t_{\text{condition1}}$
	- A simple way to check for this is to use a quantile quantile plot (QQ Plot) based on the quantiles estimated from the survival curve, if it is a straight line, then accelerated failure time holds, you can estimate 𝑎 with linear regression