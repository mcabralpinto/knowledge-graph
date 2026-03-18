*Process of quantifying physical properties (e.g., temperature) by assigning numerical values using standardized units and tools.*
## Properties
#### Resolution
The smallest difference between measurements provided by a measuring device.
#### Uncertainty
Reflects the lack of precision of the measurement (if we repeat a measurement, we will get slightly different results). There are two types:
- **Random Uncertainties**: Variations in the measurements that occur without a predictable pattern. Can be reduced but never eliminated. Must be statistically analyzed and reported in the measurement process.
- **Systematic Uncertainties**: Variations that consistently cause the measured value to be smaller or larger that the exact value (e.g., inaccurate measuring tools, miscalibration, tool reaction time/delay, etc.). Once identified, can be eliminated (one of the steps in [[Experimental Design|experiment design]]).
	- **Warm-up**: the first measurement could be different from subsequent ones 
	- **Ramp-up**: it is necessary a set of measurements to reach stable values 
	- **Hysteresis**: the outcome depends on previous measurements (history)
#### Variability
The degree to which repeated measurements under unchanged conditions show the same results. It is related to random uncertainties and can be reduced by taking multiple measurements and averaging them. Can result from two sources:
- **Precision Limitations in Instrument**: Even if the experiment conditions were totally stable, the different measurements would show slightly different values.
- **Changes in the conditions (environment, handling, etc.)**: For example, small changes in the load of a computer, cache state, available network bandwidth, etc. Quite often, the small changes in the experiment environment are analyzed statistically as random uncertainties. Extreme cases lead to outliers (that should be ignored).
#### Confidence Interval
When we perform multiple measurements of the same thing, we can calculate confidence intervals. We assume measurements are **samples from a (normal) distribution** (real value + random error), **characterize the distribution dispersion** and **find the range** that includes the desired mass of the probability density (e.g. 90%).
###### Calculation
- Let $μ$ denote the real mean of the base distribution and $\bar{x}$ the average of $n$ samples
- If the base distribution is normal, then the averages have a $t$ distribution or $Z$ distribution when sample is large ($n ≥ 30$)
- Let $α$ denote the acceptable uncertainty (imply that the level of confidence is $1~–~α$) and define the half-width as $h=t_{n-1, 1 - \alpha/2}^{S_{\bar{x}}}$, then, $p(|\bar{x}−µ|<h)=1-\alpha$
- **Intuition**: With a certainty of $1-α$ the distance between a sample of the average $\bar{x}$ and the true mean $μ$ is less than $h$ **OR** if we repeat a measurement many times, and each time we draw a segment of $±h$ around $\bar{x}$, then in $1-α$ of the cases this segment will include $μ$
Before computing CIs:
- Clean up data
- Remove data points that indicate interference or spurious measurements (top & bottom, clear outliers, etc.)
- Remove warm-up, history effects
**More in MEI slide 3!**