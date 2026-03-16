*Type of [[Evolutionary Algorithm|evolutionary algorithm]] that evolves programs or mathematical expressions (instead of fixed-size solutions). Its individuals are programs, represented as a tree, graph, or sequence.*
## Aspects
#### Representation
- **Trees**
- **Function Set**
- **Terminal Set**
#### [[Genetic Operators#Variation|Variation Operators]] 
- **Crossover**
- **Sub-Tree Mutation**
- **Recombination** (+)
#### Population Initialization
- **Full**: All nodes are functions until a certain depth, then all terminals
- **Grow**: Nodes can be functions or terminals until a certain depth
- **Ramped Half-and-Half**: Combines Full and Grow methods to create a diverse initial population
#### Preparatory Steps
- **Terminal Set**: Define the set of input variables and constants that can be used in the programs
- **Function Set**: Define the set of functions (e.g., arithmetic operations, logical operations) that can be used to build the programs
- **Fitness Function**: Define a fitness function to evaluate the performance of the programs based on the problem being solved
- **Control Parameters**: Set parameters such as population size, maximum tree depth, mutation rate, and crossover rate
- **Stopping Criteria**: Define criteria for terminating the algorithm, such as a maximum number of generations or a satisfactory fitness level
## Challenges
#### Bloat
The tendency for programs to grow in size without a corresponding improvement in fitness, leading to inefficient solutions. It leads to:
- **Protection against Genetic Operators**: Introns can protect functional code from disruptive mutations and crossover, but they can also contribute to bloat if not managed properly
- **High Computational Cost**: Evaluating the fitness of complex programs can be computationally expensive, especially for large populations and deep trees
- **Slow Execution**: Larger programs can take longer to execute, which can slow down the evolutionary process
- **Poor Readability**: Bloat can lead to programs that are difficult to understand and interpret, making it challenging to analyze the evolved solutions
###### Causal Theories
- **Introns**: Non-optimal code segments that do not affect the output but can provide genetic diversity and protect functional code from disruptive mutations
	- **Inviable Introns**: Code segments that do not contribute to the program's output
	- **Unoptimized Introns**: Code segments that contribute to the output but are not optimized for performance
- **Drift**: The phenomenon where the population's genetic makeup changes over time, which can lead to a loss of diversity and convergence to suboptimal solutions
- **Crossover Bias**: Crossover create many small, unfit, individuals. They are discarded by selection, increasing the average size of the survivors programs
###### Methods Against
- **Fitness Evaluation**: Implementing a fitness function that penalizes larger programs can help control bloat by discouraging the evolution of unnecessarily complex solutions
- **Breeding Selection**: Using selection methods that favor smaller programs can help reduce bloat by promoting the evolution of more efficient solutions (e.g., use double tournament - in the first use fitness, in the second the size)
- **Special Genetic Operators**: Select the crossover of the second parent as a function of the crossover point of the first so the corresponding sub-trees are similar
- **Survival Selection**: Fixed/dynamic limits of size and depth; operator equalization (control the distribution of programs’ lengths)
#### Overfitting
###### Solutions
- **Cross-Validation**: Use techniques like k-fold cross-validation to evaluate the performance of evolved programs on unseen data, helping to identify and mitigate overfitting
- **Parsimony Pressure**: Incorporate a penalty for program complexity in the fitness function, encouraging the evolution of simpler, more generalizable solutions
- **Early Stopping**: Monitor the performance of evolved programs on a validation set and stop the evolutionary process when performance starts to degrade, indicating potential overfitting
- **Controlling Bloat!**
## Variants
#### Grammar Evolution
- Uses a context-free grammar to define the structure of the programs, allowing for more flexible and complex program representations
#### Linear Genetic Programming
- Represents programs as linear sequences of instructions, which can be more efficient for certain types of problems (+)
#### Cartesian Genetic Programming
The genotype is a list of integers (and possibly parameters) that represent the program primitives and how they are connected together 
- CGP represents programs as graphs in which there are non-coding genes
- The genes are:
	- Addresses in data (connection genes) 
	- Addresses in a look up table of functions 
	- Additional parameters 
- This representation is very simple, flexible and convenient for many problems
- (+)