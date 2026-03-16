*Refers to the use of AI practices for the purpose of [[Entertainment|entertainment]].*
## Major Perspectives
#### 1. Rules, Grammars, & Symbolic Structure
Define a space of valid artifacts with explicit constraints $C_{valid}={c∈C:g_{j}(c)≤0~∀j}$ or generate via a grammar $G(\text{production rules})$ that guarantees validity. 
- **Pros:** interpretability, controllability, truthfulness/lore, consistency
- **Cons:** limited coverage if rules are too rigid; authoring cost
+
#### 2. Combinatorial Search & Solution Space
We define a set of possible artifacts $C$ and an objective $F(c) = \max_{\{c∈C\}} F(c)$.  Often $C$ is combinatorial (discrete) and huge. 
- **Example:** all possible levels on a grid; all possible story graphs; all NPC policies. 
- **Difficulty:** $|C|$ grows exponentially in artifact size.
+
#### 3. Learning (from Data and Feedback)
###### Supervised Learning 
Given $(x_i, y_i)$, learn $f_θ$ by: $θ^⋆=\min\limits_{θ} \sum\limits_{i} ℓ(f_θ(xi),yi)$
###### Preference/Reward Learning (pairwise) 
Given pairwise choices $c^+≻c^−$: $ϕ^⋆=\min\limits_{ϕ} \sum ℓ(s_ϕ(c^+)−s_ϕ(c^−))$
+
#### Unifying View
Different paradigms share the same pattern:
- **Rules/grammar:** sample derivations → rank by objectives 
- **Search:** explore states → keep best frontier/re-rank
- **Evolution:** mutate/crossover → select by fitness 
- **LLM:** sample sequences → re-rank/filter
[[Creativity#Co-creativity|Co-creativity]] uses all three: propose (generator), select (ranker), update (learning).
## Other
- We use [[Bayes’ Theorem]] to represent context $P(x|y)$.