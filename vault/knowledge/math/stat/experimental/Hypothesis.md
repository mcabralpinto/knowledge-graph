*A proposed explanation for a given phenomenon. Is accepted or rejected with a certain degree of certainty.*
## Properties
- **Scope**: *Abstract* (about the world) or *Concrete* (about a given design or apparatus)
- **Type**: *Explanatory* (explains, identifies relations and/or causality between variable/elements of the phenomenon) or *Predictive* (predicts the observation of a phenomenon, anticipates the outcome of an experiment, ...)
## Question Types
For **Research-Study Questions**, we have the following subtypes:
- **Exploratory**: Understand a phenomenon (subject of study) and clarify its features 
- **Base-rate**: Characterize the occurrence patterns of the phenomenon
- **Relational**: Identify possible relations of the phenomenon under study with other phenomenon 
- **Causal**: Identify cause and effect related to the phenomenon under study
For **Engineering Questions**, we have the following subtypes:
- **Design and architecture**: Define the best engineering processes and the best architecture for products 
- **Measure and optimization**: Measure and evaluate figures of merit correctly and use the measurements to optimize products and processes 
- **Benchmark and choose**: Measure to compare and choose among alternatives (components, systems, processes) 
- **Verification and validation**: Confirms that a given implementations works as specified (verification) and solves the intended problem as expected (validation)  
## Hypothesis Testing
A systematic way to test claims or ideas about a group or population, based on selected samples of such population. Follows these steps:
1. **State the hypothesis or claim to be tested**
	- **Null hypothesis ($H_0$)**: a statement about the population parameter (e.g., the population mean) that is assumed to be true.
	- **Alternative hypothesis ($H_1$)**: a statement that directly contradicts the null hypothesis by stating that the actual value of the population is not equal to the value stated in the null hypothesis.
2. **Select the criteria for a decision**
	- **Significance level**: refers to a criterion of judgment upon which a decision is made regarding the value stated in a null hypothesis. Typically 5%, meaning that if the probability of observing the sample data (or more extreme) under the null hypothesis is less than 5%, we reject the null hypothesis.
3. **Compute the test statistic**
	- **Test statistic**: a value calculated from the sample data that is used to determine whether to reject the null hypothesis. It is compared to a critical value (or used to calculate a p-value) to make a decision. Its formula is $Z_{c} = \frac{\bar{x} - μ_0}{S_{\bar{x}}}$, where $\bar{x}$ is the sample mean, $μ_0$ is the population mean under the null hypothesis, and $S_{\bar{x}} = \frac{\sigma}{\sqrt{n}}$ (standard deviation over the root of sample size) is the standard error of the sample mean.
4. **Make a decision**
	- **P-value**: the probability of observing a test statistic as extreme as, or more extreme than, the value observed in the sample data, assuming that the null hypothesis is true. If the p-value is less than the significance level, we reject the null hypothesis; otherwise, we fail to reject it.
- **Note**: We consider the data distribution normal when each execution is independent from previous executions and the variability in the measurements results from random changes in the execution conditions. If we are not sure that the data follows a normal distribution, we must test it for normality.

**Example in MEI slides 4!**
#### A More Practical Approach
1. **State the hypothesis or claim to be tested**
	- Choose a directional $H_1$ (for example, $H_1: \bar{x} < μ_0$) to make the test more powerful (i.e., more likely to reject $H_0$ when $H_1$ is true). This is a right-tailed test, so we will look for the area to the right of the test statistic
2. **Compute the test statistic**
	- $Z_{c} = \frac{\bar{x} - μ_0}{S_{\bar{x}}}$, where $S_{\bar{x}} = \frac{\sigma}{\sqrt{n}}$
3. **Obtain the p-value**
    - $p = P(Z > Z_{c})$ (for a right-tailed test)
    - To obtain $p$, look up $Z_c$ in the standard normal distribution table (or use a software function) to find the area to the right of $Z_c$
4. **Make a decision**
    - The probability of getting an average of $\bar{x}<$, assuming that the true average is $μ_0$, is $p$. If $p < 0.05$, we reject the null hypothesis with 95% confidence. This means that we have sufficient evidence to support the claim that the true average is less than $μ_0$. If $p \geq 0.05$, we fail to reject the null hypothesis, meaning that we do not have enough evidence to support the claim, and we cannot conclude that the true average is less than $μ_0$
#### Errors
- **Type I error**: Rejecting the null hypothesis when it is actually true (false positive). The probability of making a Type I error is equal to the significance level $\alpha$ (e.g., 5%).
- **Type II error**: Failing to reject the null hypothesis when it is actually false (false negative). The probability of making a Type II error is denoted by $\beta$, and the power of the test (the probability of correctly rejecting a false null hypothesis) is equal to $1 - \beta$.

It is generally seen as more serious to make a Type I error than a Type II error, as it can lead to  false claims and incorrect conclusions. Therefore, researchers often set a low $\alpha$ (e.g., 0.05) to minimize the risk of making a Type I error, while accepting a higher risk of making a Type II error.
#### T-test
Follows a Student’s T-distribution (if the null hypothesis is true) and should be applied when:
- The sample size is small (n < 30) 
- The populations’ standard deviation is not known
###### One-Sample
Used to compare a sample mean with the known population mean. Follows the same steps as the Z-test, but the test statistic is calculated as $t_{c} = \frac{\bar{x} - μ_0}{S_{\bar{x}}}$, where $S_{\bar{x}} = \frac{S}{\sqrt{n}}$ and $S$ is the sample standard deviation. The p-value is obtained from the T-distribution with $n-1$ degrees of freedom.
###### Two-Sample
Used to compare the means of two independent samples. The test statistic is calculated as $t_{c} = \frac{\bar{x}_1 - \bar{x}_2 + Δ}{S_{\bar{x}_1 - \bar{x}_2}}$, where $Δ$ is the hypothesized difference between the population means (often 0 for testing equality) and $S_{\bar{x}_1 - \bar{x}_2} = \sqrt{\frac{S_1^2}{n_1} + \frac{S_2^2}{n_2}}$ is the standard error of the difference between the two sample means. The p-value is obtained from the T-distribution with degrees of freedom calculated using the Welch-Satterthwaite equation.

**Example in MEI slides 5!**
#### Effect Size
A measure of the magnitude of the difference between groups or the strength of a relationship between variables. It provides information about the practical significance of the results, beyond just statistical significance. Reporting effect sizes helps to understand the real-world impact of findings and allows for comparisons across studies. Common measures of effect size include:
- Cohen's $d$: measures the standardized difference between two means. It is calculated as $d = \frac{\bar{x}_1 - \bar{x}_2}{s_p}$, where $\bar{x}_1$ and $\bar{x}_2$ are the sample means of the two groups, and $s_p$ is the pooled standard deviation. Cohen's $d$ values of 0.2, 0.5, and 0.8 are often interpreted as small, medium, and large effect sizes, respectively.
- Pearson's r
- Odds ratios. 