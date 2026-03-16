*Techniques used to prevent [[Overfitting|overfitting]] by penalizing complex models, thereby improving generalization to new, unseen data.*
## Types
#### L1 Regularization (Lasso)
Adds a penalty proportional to the absolute value of weights: $$Loss = Original~Loss + \lambda \sum_{i=1}^{N} |w_i| $$Encourages sparsity in weights (many weights become exactly zero), leading to simpler models that may ignore irrelevant features. Useful for feature selection.
#### L2 Regularization (Ridge)
Adds a penalty proportional to the square of weights: $$Loss = Original~Loss + \lambda \sum_{i=1}^{N} w_i^2 $$Encourages smaller weights but does not enforce sparsity (weights get close to zero). Helps distribute weight more evenly across features, reducing the impact of any single feature.
#### Dropout
During training, randomly "drops" (sets to zero) a fraction of neurons in each layer. This forces the to not rely too heavily on specific neurons, effectively creating an ensemble of different network architectures, improving generalization.