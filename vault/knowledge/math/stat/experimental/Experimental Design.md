*Process of systematically defining and planning [[Experiment|experiments]] in such a way that the date obtained can be analyzed to draw valid and objective conclusions.*

The goal is to design and perform valid experiments that allow good technical decisions: characterize and optimize process/product decisions. Its basic idea is the following:
- **Introduce controlled changes** to input variables in order to to study their effect on an observable variable (or variables)
- **Get the maximum amount of information** on cause and effect relationships with the minimum effort
## Process
An eight step process is followed for [[Experiment Types#Controlled Experiment|controlled/laboratory experiments]]:
1. Problem statement (or research question) 
2. Identify variables 
3. Generate hypothesis 
4. Define the experimental setup/scenario 
5. Develop tools and procedures for the experiment 
6. Run experiments and collect the data/measurements 
7. Perform data analysis 
8. Draw conclusions *(often go back to the beginning and reformulate the problem statement or test a different hypothesis)*
#### Problem Statement
A good (i.e., relevant) problem statement should be focused enough to allow the clear identification of the variables of the problem but, at the same time, should be sufficiently open to allow different hypothesis to answer the problem/question. A possible generic formulation could be: *How does X affect Y under conditions Z?*
To formulate good problem statements, one must: 
- Know the subject area: process, system, technique, product, product market, etc.
- Be precise and clear
- Be sure that the problem/question is relevant
#### Variable Identification
Different types of variables are identified in an experiment:
- **Dependent variable (response variable):** Measured output (e.g., response time, throughput, no. bugs, downtime, latency, error detection coverage, etc.)
- **Independent variables (factors):** Input variables that can be changed in the experiment (e.g., memory size, clock rate, file size, channel bandwidth, etc.)
- **Levels:**  Values taken by the variables. Can be (nearly) continuous (e.g., ~time, size in bytes) or discrete (type of system, type of algorithm, etc.)
The experience methodology may require each variable to be changed individually (**one at a time**) or to change several variables at the same time (**full factorial**). The latter allows to study interactions between variables but requires more experiments.
###### Terminology
- **Baseline / Golden Run:** A reference point for comparison (of independent variable values), often representing the current state of the system or a standard configuration. It serves as a benchmark to evaluate the effects of changes in independent variables.
- **Golden Run Repetition:** Repeating the baseline experiment multiple times to account for variability and ensure that observed effects are due to changes in independent variables rather than random fluctuations.
- **Randomization:** Minimize potential uncontrollable biases in the experiments by randomly assigning factors to “average out” the effects of possible extraneous factors. 
- **Blocking:** The experiment is divided in homogeneous segments (blocks like sets of machines, users, loads, etc.) to improve precision. The goal is to control the variability block to block.
- **Confounding variable:** Extraneous variable that influences the relationship between the dependent and independent variables (i.e., correlates with both the dependent and independent variables).
#### Hypothesis Generation
Hypothesis describe provisional relationships between factors (independent variables) and the response variable (dependent). 
- It is an provisional answer to the problem statement
- It can be directional or non-directional (whether it attributes a value (scale, positive vs. negative, etc.) to the predicted relation between variables)
- It is always pair: 
	- **Null hypothesis ($H_0$)** states that there is no effect, no difference, or no relationship between the variables being studied.
	- **Alternate hypothesis ($H_1$)** states that there is an effect, a difference, or a relationship.
###### Example 
$H_0$: There is no difference between the execution time of algorithm A and B
$H_1:$ The execution time of algorithm A is shorter than B (*directional*)
#### Result Collection
- Measurements may be continuous or discrete
- [[Performance Metric|Performance metrics]] are often used
#### Data Analysis
May be **exploratory** (e.g., visualizations, descriptive statistics, etc.) or **statistical** (e.g., hypothesis testing, regression, etc.). The goal is to determine whether the observed effects are statistically significant and to draw conclusions about the relationships between variables.