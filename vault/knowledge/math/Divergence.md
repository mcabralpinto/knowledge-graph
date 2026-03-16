*Function that measures how different one [[Probability Distribution|probability distribution]] is from another.*
## Kullback-Leibler Divergence (KL Divergence)
Measures the difference between two probability distributions $P$ and $Q$:
- It quantifies how much information is lost when $Q$ is used to approximate $P$. 
- It is not symmetric, meaning that $D_{KL}(P || Q)$ is not the same as $D_{KL}(Q || P)$. It is always non-negative, and a value of 0 indicates that the two distributions are identical. 
- KL divergence is commonly used in machine learning for tasks such as variational inference and generative modeling, where it helps to measure how well a model's predicted distribution matches the true data distribution.
- Its formula is: $$D_{KL}(P || Q) = \sum_{x} P(x) \log \left( \frac{P(x)}{Q(x)} \right)$$Where $P(x)$ and $Q(x)$ are the probabilities of event $x$ under distributions $P$ and $Q$, respectively. 
#### Jensen-Shannon Divergence (JS Divergence)
A symmetric and smoothed version of KL divergence that measures the similarity between two probability distributions $P$ and $Q$:
- JS divergence is always between 0 and 1, where 0 indicates that the distributions are identical and 1 indicates that they are completely different. 
- It is often used in machine learning for tasks such as clustering and generative modeling, where it provides a more stable and interpretable measure of similarity between distributions compared to KL divergence.
- It is defined as: $$D_{JS}(P || Q) = \frac{1}{2} D_{KL}(P || M) + \frac{1}{2} D_{KL}(Q || M)$$Where $M = \frac{1}{2}(P + Q)$ is the average of the two distributions. 
## Wasserstein Distance (Earth Mover's Distance)
Measures the distance between two probability distributions $P$ and $Q$ by calculating the minimum cost of transforming one distribution into the other:
- It is based on the concept of moving "mass" from one distribution to another, where the cost is defined as the amount of mass moved multiplied by the distance it is moved. 
- Wasserstein distance is particularly useful in machine learning for tasks such as generative modeling and optimal transport, as it provides a more meaningful measure of distance between distributions, especially when they have non-overlapping support. 
- It is defined as: $$W(P, Q) = \inf_{\gamma \in \Gamma(P, Q)} \mathbb{E}_{(x, y) \sim \gamma} [d(x, y)]$$Where $\Gamma(P, Q)$ is the set of all joint distributions $\gamma$ with marginals $P$ and $Q$, and $d(x, y)$ is the distance between points $x$ and $y$ in the underlying space.