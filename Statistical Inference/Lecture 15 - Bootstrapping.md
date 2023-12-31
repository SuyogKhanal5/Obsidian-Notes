
- ### Think More
	- ###### To get the distribution of sample proportion from last lecture  
		- The population was known ($900$ out of $2400$ red balls)  
		- Draw one sample with sample size $n=50$  
		- Repeat the experiment $m$ times (for example, $m=1000$)  
	- ###### Realistic questions  
		- Do we know the population?  
		- Do we want to (or can we) repeat $m$ times?

- ### Practical Problem
	- The average year on US pennies in 2019  
	- ###### Population: all pennies on market in 2019  
		- Do we know the population?  
		- Can we have the population?  
	- ###### Sample: $50$ pennies from a local bank  
		- Record the year on each penny  
		- Calculate the mean year  
		- Do we want to (can we) repeat this multiple times?

- ### Bootstrapping
	- ###### Pull yourself up by your bootstraps
		- Originally "Why can not a man lift himself by pulling up on his bootstraps?"
		- Satirical saying, impossible achievement
		- Evolves to mean that something is possible with individual effort
	- ###### Bootstrapping
		- Resampling technique
		- Start from original sample
		- Draw *with replacement*
		- The *same sample size* as the original
	- Different types of bootstrapping methods
	- ###### Bootstrapping vs. Monte Carlo
		- Both are based on repetitive sampling
		- **Bootstrapping**: Resample from original sample, a nonparametric approach
		- **Monte Carlo**: Setting up a data generation procedure with known parameters
	- ###### Bootstrapping vs. Jackknife
		- Both are resampling techniques
		- **Jackknife**: Form a sample by deleting one or more observations each time

- ### How to Draw with Replacement with Same Sample Size
	- Need to draw one each time, put it back, repeat $n$ times
	- Virtual Sampling: `rep_sample_n(size, replace=TRUE)`![[Pasted image 20231031020600.png]]

- ### Virtual Sampling Example
	- Could end up with duplicates![[Pasted image 20231031020633.png]]

- ### Penny Example - Manual Sampling
	- ###### Original Sample
		- Saved as `pennies_sample` in `moderndive` package
		- Sample size $n=50$, `year` is recorded
	- ###### Resamples
		- Manually sampled $35$ times, each time with sample size $n=50$
		- Saved as `pennies_resamples`
			- $35 \cdot 50 = 1750$ observations
			- The person's `name` who did manual sampling was also recorded
		- Why do we need to resample $35$ times?
			- What we are interested in is the average year, resampling once only gives you one average
			- Need the distribution of the sample statistic (sample mean)
	- ###### Distribution of the Year![[Pasted image 20231031020947.png]]
	- ###### Distribution of Year vs. Mean Year![[Pasted image 20231031021009.png]]
	- ###### Summary Statistics
		- `year`: Original sample with $50$ pennies![[Pasted image 20231031021046.png]]
		- Resample $35$ times, $35$ `meanyear` values![[Pasted image 20231031021112.png]]
		- `meanyear`: From $35$ repetitions![[Pasted image 20231031021140.png]]
	- ###### Bootstrap Distribution Manual / Virtual Sampling![[Pasted image 20231031021208.png]]
		- ###### What Do We Observe?
			- Distribution of `year` from original sample and `meanyear` from $35$ resamples
				- Are the means close enough to each other?
				- How about the variances?
			- Much difference between manual samples and virtual ones?
			- Virtual Sampling
				- Will the number of repetitions change the distribution?
				- What is the shape of the distribution?

- ### Terminologies
	- ###### Sample Distribution
		- The distribution of a sample
			- Ex. distribution of red balls, distribution of year in pennies
	- ###### Sampling Distribution
		- The distribution of sample statistics
			- Ex. distribution of proportion of red balls, distribution of average years in the pennies
	- ###### Bootstrap Distribution
		- One type, or one approximation to sampling distribution
		- Achieved by bootstrap method

- ### Additional Notes
	- ###### Random Seed
		- `set.seed(n)` in R
		- Make sure the results don't change each time
		- Ensure reproducibility of your work
	- ###### Population
		- Each row should be unique
			- Unique ID
		- Identify duplicates
			- Check distribution of ID
			- `duplicated()`: Returns `TRUE` or `FALSE` for each row
		- Eliminate duplicates
			- `distinct()`: Remove duplicates based on all variables
			- `distinct(col1, col2, ...)`: Remove duplicates based on specified 