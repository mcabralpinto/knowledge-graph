*Coefficients that consider the possibility of user agreeing by chance for categorical items (relevant for crowdsourcing).*

It is generally thought to be a more robust measure than simple percent agreement calculation, as $\kappa$ takes into account the agreement occurring by chance.
### Cohen's Kappa (for 2 annotators)
##### Formula
The formula for Cohen's Kappa is: $$ \kappa = \frac{p_o - p_e}{1 - p_e} $$$p_o$ is the relative observed agreement among raters (proportion of times that users agree): $$p_o = \frac{\text{Number of agreements}}{\text{Total number of items}}$$$p_e$ is the hypothetical probability agreement by chance, using the observed data to calculate the probabilities of each observer randomly saying each category: $$ p_e = \sum_{i=1}^{k} (p_{i_1} \times p_{i_2}) $$
$k$ is the number of categories, $p_{i_1}$ and $p_{i_{2}}$ are the marginal probabilities of each rater assigning items to the $i$-th category.
##### Interpretation
| Kappa Range                    | Interpretation           |
| ------------------------------ | ------------------------ |
| $\kappa < 0$                   | No agreement             |
| $0.01 \leq \kappa \leq 0.20$   | Slight agreement         |
| $$0.21 \leq \kappa \leq 0.40$$ | Fair agreement           |
| $$0.41 \leq \kappa \leq 0.60$$ | Moderate agreement       |
| $$0.61 \leq \kappa \leq 0.80$$ | Substantial agreement    |
| $$0.81 \leq \kappa \leq 1.00$$ | Almost perfect agreement |
