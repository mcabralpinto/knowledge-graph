*Techniques used in [[Genetic Algorithm|genetic algorithms]] to find optimal solutions by mimicking natural evolution.*
## Selection
#### Tournament Parent Selection
Randomly select a group of individuals from the population and choose the best among them for reproduction. This method is simple and effective, providing a balance between exploration and exploitation.
```python
# do with a subset of the population
def tournament_selection(pop, fit_values, size):
    selected_individuals = []
    for _ in range(len(pop)):
        tournament = random.sample(list(zip(pop, fit_values)), size)
        winner = max(tournament, key=lambda x: x[1])  # select highest fitness
        selected_individuals.append(winner[0])
    return selected_individuals
```
#### Roulette Wheel Parent Selection
Individuals are selected with a probability proportional to their fitness. This method can lead to premature convergence if one individual has significantly higher fitness than the others, as it may dominate the selection process.
```python
# do with a subset of the population
def roulette_wheel_selection(pop, fit_values):
    total_fitness = sum(fit_values)
    selection_probs = [f / total_fitness for f in fit_values]
    selected_individuals = random.choices(pop, weights=selection_probs, k=len(pop))
    return selected_individuals
```
#### Elitism
The best individuals are guaranteed to be selected for the next generation, ensuring that the best solutions are preserved. This method can be combined with other selection techniques to maintain diversity while ensuring that the best solutions are not lost.
```python
def elitism(pop, fit_values, n): # n -> number of elites to select
    elites = sorted(zip(pop, fit_values), key=lambda x: x[1], reverse=True)[:n]
    selected_individuals = [elite[0] for elite in elites]
    return selected_individuals
```
## Variation
#### Crossover
Crossover is a genetic operator used to combine the genetic information of two parent individuals to create offspring. It is a key mechanism in genetic algorithms that promotes the exchange of genetic material and helps to explore the solution space. There are various types of crossover techniques, including:
- **One-point Crossover**: A single crossover point is selected, and the genetic material is exchanged between the two parents at that point
- **Two-point Crossover**: Two crossover points are selected, and the genetic material between these points is exchanged between the parents
- **Uniform Crossover**: Each gene is independently selected from either parent with equal probability, allowing for a more diverse combination of genetic material
- **Order Crossover**: For permutation representations, a subsequence of genes is selected from one parent and the remaining genes are filled in from the other parent while maintaining the order of genes
- **Partially Mapped Crossover (PMX)**: For permutation representations, a partial mapping is created between the two parents to ensure that offspring are valid permutations (**see IAIN slide 5**)
- **Cycle Crossover**: For permutation representations, cycles of genes are identified between the two parents, and offspring are created by alternating these cycles between the parents
###### Real-valued representations
- **Arithmetic Crossover**: Offspring are created by taking a weighted average of the parents' genes: $x' = α×x_1+(1−α)×x_2$, $α ∈ [0,1]$
- **Heuristic Crossover**: Offspring are created by extrapolating beyond the better parent $x_1$ in the direction of worse parent $x_2$: $x' = x_1 + r(x_1 - x_2)$, $r ∈ [0,1]$
#### Mutation
Mutation is a genetic operator that introduces random changes to an individual's genetic material. It is used to maintain genetic diversity within the population and to explore new areas of the solution space. Mutation can be implemented in various ways, such as:
- **Bit Flip Mutation**: For binary representations, randomly flip a bit from 0 to 1 or vice versa.
- **Random Resetting**: For integer representations, randomly change a gene to a different value within the allowed range.
- **Gaussian / Uniform Mutation**: For real-valued representations, add a small random value drawn from a [[Probability Distribution|distribution]] to a gene.
###### Permutations
- **Swap Mutation**: For permutation representations, randomly select two genes and swap their positions.
- **Insertion Mutation**: For permutation representations, randomly select a gene and insert it at a different position in the sequence.
- **Inversion Mutation**: For permutation representations, randomly select a subsequence of genes and reverse their order.