*Type of [[Markov Model|Markov model]] describing systems composed of observable events that move between different states (like weather).*
## Assumptions
- **First-order Process:** The future is independent of the past given the present:
$$ P(X_{t} | X_{1:t-1}) = P(X_{t} | X_{t-1}) $$
- **$k$-order Process:** The future depends on the last $k$ states:
$$ P(X_{t} | X_{1:t-1}) = P(X_{t} | X_{t-1}, \dots, X_{t-k}) $$
- **Stationary Process:** Transition model is time-invariant:
$$ P(X_{t} | X_{t-1}) = P(X_{t+1} | X_{t}) $$
- **Sensor:** Evidence at time $t$ depends only on the current state:
$$ P(E_t | X_{1:t}, E_{1:t-1}) = P(E_t | X_t) $$
First-order not necessarily true in the real world!
## Inference Tasks
- **Filtering:** Given evidence up to time $t$, what is the belief state (distribution over current states)?
$$ P(X_t | E_{1:t}) $$
- **Prediction:** Given evidence up to time $t$, what is the belief state at time $t+k$?
$$ P(X_{t+k} | E_{1:t}) $$
- **Smoothing:** Given evidence up to time $t$, what is the belief state at time $k < t$? 
$$ P(X_k | E_{1:t}) $$
- **Most Likely Explanation:** Given evidence up to time $t$, what is the most likely sequence of states?
$$ \arg\max_{X_{1:t}} P(X_{1:t} | E_{1:t}) $$
## Filtering Algorithm
1. **Initialization:** Start with prior belief $P(X_0)$.
2. **Prediction Step:** For each time step, predict the next state using the transition model:
$$ P(X_t | E_{1:t-1}) = \sum_{x_{t-1}} P(X_t | X_{t-1}) P(X_{t-1} | E_{1:t-1}) $$
3. **Update Step:** Incorporate the new evidence to update the belief state ($\alpha$ is a normalization constant):
$$ P(X_t | E_{1:t}) = \alpha P(E_t | X_t) P(X_t | E_{1:t-1}) $$
## Prediction Algorithm
1. **Initialization:** Start with prior belief $P(X_0)$.
2. **Iterative Prediction:** For each time step up to $t+k$, apply the prediction step:
$$ P(X_{t+i} | E_{1:t}) = \sum_{x_{t+i-1}} P(X_{t+i} | X_{t+i-1}) P(X_{t+i-1} | E_{1:t}) $$
## Smoothing Algorithm
1. **Forward Pass:** Cache the filtered beliefs $P(X_t | E_{1:t})$ for all $t$. 
2. **Backward Pass:** For each time step from $t-1$ down to $k$, update the belief state using future evidence:$$ P(X_k | E_{1:t}) = P(X_k | E_{1:k}) P(E_{k+1:t} | X_k) $$
## MLE - Viterbi Algorithm
1. **Initialization:** Set up a table to store the maximum probabilities and backpointers.
2. **Recursion:** For each time step and state, compute the maximum probability of reaching that state from any previous state $$ m_{1:t} = P(e_t | X_t) \times \max_{X_{t-1}} (P(X_t | X_{t-1}) \times m_{1:t-1}) $$
3. **Termination:** Identify the maximum probability in the last column and backtrack to find the most likely state sequence.