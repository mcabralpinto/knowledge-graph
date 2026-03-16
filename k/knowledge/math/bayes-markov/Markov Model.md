*A general category of mathematical models for random processes (stochastic processes) that exhibit the Markov Property (future depends only on the present).*

The world changes; we need to track and predict it. We can copy state and evidence variables for each time step (assuming discrete time):
- $X_t$ $\rightarrow$ set of unobservable state variables at time $t$ (e. g. blood sugar, stomach contents)
- $E_t$ $\rightarrow$ set of observable evidence variables at time $t$ (e. g. measured blood sugar, food eaten)
- Notation: $X_{a:b}$ =  $X_a, X_{a+1}, ..., X_b$.
## Markov Property
The future state depends only on the current state (or the last N−1 states):
$$P(x_t |x_1,x_2,...,x_{t−1})≈P(x_t |x_{t−n+1},...,x_{t−1})$$
## Types
- **[[Markov Chain]]**
- **[[Hidden Markov Model]]**
- ...