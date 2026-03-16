*Directed acyclic graph that represents variables and their conditional dependencies.*

A Bayesian Network represents [[Bayes’ Theorem#Naive Bayes|conditional independence]] assertions in a variable space, allowing for a compact specification of Full Joint Distributions. A regular FJD table's parameter number grows exponentially with the number of variables ($O(2^n)$), while a Bayesian Network can represent the same distribution more compactly by exploiting conditional independencies ($O(n \times 2^k)$) for a BN whose nodes have a maximum of $k$ parents).
## Concepts
- **Global Semantics:** defines the full joint distribution as the product of the local conditional distributions: $$P(X_1, X_2, ..., X_n) = \prod_{i=1}^{n} P(X_i | Parents(X_i))$$
- **Local Semantics:** each node is conditionally independent of its non-descendants given its parents: $$P(X_i | Parents(X_i), NonDescendants(X_i)) = P(X_i | Parents(X_i))$$Equivalent to Global Semantics (we can reconstruct each from the other).
- **Markov Blanket:** the minimal set of nodes that renders a node conditionally independent from the rest of the network. It consists of the node's parents, children, and children's other parents.
## Dynamic BNs
Extend BNs to model sequences of variables over time, representing temporal processes. Each time slice contains variables that depend on the previous slice, allowing for modeling of time-series data.