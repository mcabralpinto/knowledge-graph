*List of statistical measures.*
## **Variance** 
Measures how spread out data points are from their average. Calculated as the average of the square differences from the mean.  $$\sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2$$Where $N$ is the number of data points, $x_i$ are the data points, and $\mu$ is the mean.
#### Standard Deviation
The square root of variance, providing a measure of spread in the same units as the data. $$\sigma = \sqrt{\sigma^2}$$
## **Covariance** 
Indicates the direction of the linear relationship between two variables. A positive covariance means that as one variable increases, the other tends to increase as well, while a negative covariance indicates that as one variable increases, the other tends to decrease. $$\text{Cov}(X, Y) = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu_X)(y_i - \mu_Y)$$Where $N$ is the number of data points, $x_i$ and $y_i$ are the data points of variables $X$ and $Y$, and $\mu_X$ and $\mu_Y$ are their respective means.
## **Correlation**
Measures the strength and direction of the linear relationship between two variables. It is a normalized version of covariance, ranging from -1 to 1. A correlation of 1 indicates a perfect positive linear relationship, -1 indicates a perfect negative linear relationship, and 0 indicates no linear relationship. $$r = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}$$Where $\text{Cov}(X, Y)$ is the covariance of variables $X$ and $Y$, and $\sigma_X$ and $\sigma_Y$ are their standard deviations.
## Signal-to-Noise Ratio (SNR)
Measures the strength of a signal relative to background noise. It is often expressed in decibels (dB) and calculated as: $$\text{SNR} = 10 \log_{10} \left( \frac{P_{\text{signal}}}{P_{\text{noise}}} \right)$$Where $P_{\text{signal}}$ is the power of the signal and $P_{\text{noise}}$ is the power of the noise. A higher SNR indicates a clearer signal with less noise interference.