*Function, table, or graph that shows all possible values for a variable and how often they occur (frequency or probability).*
## Types
#### Uniform Distribution $U(a, b)$
A distribution where all outcomes are equally likely. For example, rolling a fair six-sided die has a uniform distribution because each outcome (1, 2, 3, 4, 5, 6) has an equal probability of 1/6.
- **Probability Density Function (PDF)**: $f(x) = \frac{1}{b - a}$ for $a \leq x \leq b$, and 0 otherwise
###### Parameters
- $a$: The minimum value of the distribution
- $b$: The maximum value of the distribution
```chart  
type: line
labels: [1,2,3,4,5,6]
series:
- label: "Probability Density Function f(x)"
  data: [0.1667, 0.1667, 0.1667, 0.1667, 0.1667, 0.1667]
  borderColor: "rgb(75, 192, 192)"
  tension: 0.1
  fill: false
options:
  xAxis:
    title:
      display: true
      text: "x"
  yAxis:
    title:
      display: true
      text: "f(x)"
    suggestedMin: 0
    suggestedMax: 0.15
```
#### Normal Distribution $N(\mu, \sigma^2)$
A bell-shaped distribution that is symmetric around the mean. It is characterized by its mean (average) and standard deviation (spread). Many natural phenomena, such as heights of people or test scores, follow a normal distribution.
- **Probability Density Function (PDF)**: $f(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}$
###### Parameters
- $\mu$: The mean of the distribution
- $\sigma^2$: The variance of the distribution (the square of the standard deviation)
```chart  
type: line
labels: [-3, -2.5, -2, -1.5, -1, -0.5, 0, 0.5, 1, 1.5, 2, 2.5, 3]
series:
  - label: "Probability Density Function f(x)"
    data: [0.0044, 0.0175, 0.0539, 0.1295, 0.2419, 0.3521, 0.3989, 0.3521, 0.2419, 0.1295, 0.0539, 0.0175, 0.0044]
    borderColor: "rgb(255, 99, 132)"
    tension: 0.4
    fill: false
options:
  xAxis:
    title:
      display: true
      text: "x"
  yAxis:
    title:
      display: true
      text: "f(x)"
    suggestedMin: 0
    suggestedMax: 0.5
    

```
#### Binomial Distribution $B(n, p)$
A distribution that describes the number of successes in a fixed number of independent trials, each with the same probability of success. For example, flipping a coin 10 times and counting the number of heads follows a binomial distribution.
- **Probability Mass Function (PMF)**: $P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$ for $k = 0, 1, 2, ..., n$
###### Parameters
- $n$: The number of trials
- $p$: The probability of success on each trial
```chart  
type: bar
labels: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
series:
  - label: "Probability Mass Function P(X = k)"
    data: [0.00098, 0.00977, 0.04395, 0.11719, 0.20508, 0.24609, 0.20508, 0.11719, 0.04395, 0.00977, 0.00098]
    backgroundColor: "rgba(255, 159, 64, 0.5)"
    borderColor: "rgba(255, 159, 64, 1)"
    borderWidth: 1
options:
  xAxis:
    title:
      display: true
      text: "k (number of successes)"
  yAxis:
    title:
      display: true
      text: "P(X = k)"
    suggestedMin: 0
    suggestedMax: 0.3
```
#### Poisson Distribution $P(\lambda)$
A distribution that describes the number of events occurring in a fixed interval of time or space, given a constant average rate of occurrence. For example, the number of emails received in an hour can be modeled using a Poisson distribution.
- **Probability Mass Function (PMF)**: $P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$ for $k = 0, 1, 2, ...$
###### Parameters
- $\lambda$: The average number of events in the given interval
```chart  
type: bar
labels: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
series:
  - label: "Probability Mass Function P(X = k)"
    data: [0.3679, 0.3679, 0.1839, 0.0613, 0.0153, 0.0031, 0.0005, 0.0001, 0.00001, 0.000001, 0.0000001]
    backgroundColor: "rgba(153, 102, 255, 0.5)"
    borderColor: "rgba(153, 102, 255, 1)"
    borderWidth: 1
options:
  xAxis:
    title:
      display: true
      text: "k (number of events)"
  yAxis:
    title:
      display: true
      text: "P(X = k)"
    suggestedMin: 0
    suggestedMax: 0.4
```