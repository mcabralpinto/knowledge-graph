*In [[Co-Creativity|co-creativity]], generation refers to the process of creating and producing digital media.*
## Design Space
We have:
- **Artifacts**: $c∈C$ (levels, scenes, motions, etc.)
- **Hard Constraints**: $g_j(c)≤0$ (playability, budget, lore, safety)
- **Soft Objective**: $F(c;x)$ (difficulty, pacing, aesthetics, personalization)
#### Views
- **Optimization**: $\max\limits_{c∈C} F(c;x)$ subject to $g_j(c)≤0$
- **Probabilistic $\rightarrow$ Sampling + Selection**: $c∼q_\theta(c|x)$, then select by ranking ($q_\theta$ is a distribution parameterized by $\theta$ that we want to learn to approximate the optimal artifact distribution)
- **Lagrangian**: $\max\limits_{c∈C} F(c;x) - \sum_j λ_{j} max(0, g_j(c))$ ($λ_{j}$ is a penalty parameter that balances the objective and the constraints). This converts constrained problem into a single scalar score. Works for search, reranking, and learned reward models.
#### Validity vs. Quality
- **Validity**: $g_j(c)≤0$ (playability, budget, lore, safety) - satisfies constraints
- **Quality**: $F(c;x)$ (difficulty, pacing, aesthetics, personalization) - optimizes objectives
- **Engineering Stance**: hard constraints first (filter/repair), then rank/re-rank for quality.
## Families
#### 1. Rule-based Models - Grammars & Symbolic Structure
Define a space of valid artifacts with explicit constraints $C_{valid}={c∈C:g_{j}(c)≤0~∀j}$ or generate via a [[Grammar|grammar]] $G(\text{production rules})$ that guarantees validity. 
- **Pros:** interpretability, controllability, truthfulness/lore, consistency
- **Cons:** limited coverage if rules are too rigid; authoring cost
###### Probabilistic CFG (PCFG)
Add rule probabilities $p(r|A)$, $\sum\limits_{r} p(r|A) = 1$ to a [[Grammar#Context Free Grammar|CFG]]. This defines a distribution over derivations $d$ and outputs $c$ (multiple derivations can yield the same $c$ - ambiguity): $$q_{G}(c) = \sum\limits_{d\text{: yield(}d\text{)}= c} \prod\limits_{r∈d} p(r|A)$$
It can be sampled using a simple algorithm:
```python
def sample(G, A):
	r = sample(p(r|A)) # sample a rule for non-terminal A
	c = []
	for symbol in r: # for each symbol in the rule
		if symbol is non-terminal:
			c.extend(sample(G, symbol)) # rec. sample for non-terminals
		else:
			c.append(symbol) # add terminal symbols to output
	return c
```
(+) constrained sampling
#### 2. Statistical Models - Markov Chains & N-grams
Before deep learning, [[Probability Distribution|probability distributions]] over sequences were modeled using [[Markov Model#Markov Property|Markov properties]]. Useful for procedural names, simple music, or terrain.
#### 3. Search-Based PCG
Implies generation as optimization in a combinatorial design space. The rationale is: evaluate candidates, keep improving.
- **State-Space Formalism**: defined as a tuple $(S,A,T,s_0,G)$:
    - $S$: set of states (partial/complete artifacts)
    - $A$: set of actions (modifications to the artifact)
    - $T$: transition function $T(s,a) → s'$ (how actions change the artifact)
    - $s_0$: initial state (empty or seed artifact)
    - $G$: goal condition(or objective threshold $F(s)>θ$)
###### Constructive Search
Constructing an artifact piece-by-piece:
- **[[Search Algorithm|A*]] Search**: uses a heuristic to estimate the cost to reach the goal from a given state, guiding the search towards promising areas of the state space.
- **[[Search Algorithm|Beam Search]]**: keeps track of the top $k$ best states at each level of the search tree, allowing for a more focused exploration of the state space while still maintaining diversity.
###### Local Search
Iteratively improve a complete artifact by making local modifications:
- **[[Meta-Heuristics#Hill Climbing|Hill Climbing]]**: iteratively moves to the best neighboring state, which can lead to local optima.
- **[[Meta-Heuristics#Simulated Annealing|Simulated Annealing]]**: allows for occasional moves to worse states to escape local optima, with a cooling schedule that reduces the probability of such moves over time.
	- **Acceptance Probability**: $$P(accept) = \begin{cases} 1 & \text{if } F(s') > F(s) \\ e^{\frac{F(s') - F(s)}{T}} & \text{if } F(s') ≤ F(s) \end{cases}$$
    where $s$ is the current state, $s'$ is the candidate state, $F$ is the objective function, and $T$ is the current temperature.
###### [[Evolutionary Algorithm|Evolutionary Algorithms]]
Inspired by natural selection, these algorithms maintain a population of candidate solutions that evolve over time through selection, crossover, and mutation. They are particularly effective for complex, high-dimensional, or poorly understood search spaces.
- **Selection**: Choose individuals based on fitness (objective function value) to be parents for the next generation.
- **Crossover**: Combine parts of two or more parents to create offspring, promoting the exchange of good traits.
- **Mutation**: Introduce random changes to individuals to maintain diversity and explore new areas of the search space.
###### Monte Carlo Tree Search (MCTS)
Balances exploration and exploitation by building a search tree based on random sampling of the search space. It is particularly effective for sequential decision-making problems, such as game level generation or story generation. It uses the following **Upper Confidence Bound for Trees (UCT)**: $$UCT_{i} = \frac{W_{i}}{N_{i}} + c \sqrt{\frac{\ln N_{p}}{N_{i}}}$$
Where $W_{i}$ is the total reward of node $i$, $N_{i}$ is the number of times node $i$ has been visited, $N_{p}$ is the number of times parent $p$ has been visited, and $c$ is a constant that balances exploration and exploitation.
1. **Selection**: Traverse tree picking max UCT. 
2. **Expansion**: Add a new child node.
3. **Simulation**: Random rollout to a terminal state.
4. **Backpropagation**: Update $W_i$ and $N_i$ up the tree.
#### 4. Learned Generators
Use [[Machine Learning|machine learning]] to learn a generator $q_\theta(c|x)$ that can produce high-quality artifacts directly from large datasets. The generator can be trained using supervised learning (if we have examples of good artifacts) or reinforcement learning (if we can evaluate the quality of generated artifacts). Great expressiveness; needs control and verification.
- **[[Generative Adversarial Network]]**
- **[[Autoregression|Autoregressive]] Generation ([[Large Language Model|LLMs]]) for text**: Models build artifacts sequentially:$$p(x_{1:T}|c) = \prod\limits_{t=1}^{T} p(x_t|x_{<t},c)$$	
	- **Generation**: Handled via Beam Search, Top-k, or Top-p sampling. 
	- **Curation**: Ranker/re-ranker selects coherent, safe, style-aligned outputs.
- **[[Diffusion Model|Diffusion Models]] for images**:
	- **Forward Process**: Gradually add noise to an image $x_0$ over $T$ steps: $$q(x_t|x_{t-1}) = N(x_t; \sqrt{1-β_t} x_{t-1}, β_t I)$$
	- **Reverse Process**: Learn to denoise from $x_T$ back to $x_0$: $$p_θ(x_{t-1}|x_t) = N(x_{t-1}; μ_θ(x_t, t), σ^2 I)$$
	- **Generation**: Sample $x_T$ from noise, then iteratively apply the reverse process to get $x_0$ (the generated image). Conditioning can be added by modifying $μ_θ$ to depend on additional inputs (e.g., text prompts)
	- Used for sprites, textures, concept boards

EXAMPLES AT THE END OF IAE SLIDES 5!