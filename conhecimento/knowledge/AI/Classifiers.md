*List of classifiers used in ML approaches.*
###### **Minimum Distance Classifier**
Computes centroids (mean vector of all the features vectors) for each class in the training set and assigns labels to test samples based on the nearest centroid. Can use different distance functions, such as:
- **Euclidian:** Straight-line distance between points in the feature space.
- **Mahalanobis:** Distance between a point and a distribution, accounting for the covariance structure of the data. It is more robust to correlated features and differences in feature scaling when compared to Euclidean distance. For a mean vector $μ$, a data point $x$, and a [[Covariance Matrix||covariance matrix]] $Σ$, its formula is $D_M = \sqrt{(x - \mu)^T \Sigma^{-1} (x - \mu)}$. Intuitively, the inverse covariance $Σ^{-1}$ “widens” the data: correlated directions are decorrelated (aligned with the covariance eigenvectors) and each direction is scaled by the inverse of its variance (eigenvalues).
###### **Fisher LDA Classifier**
Based on [[Feature Selection & Reduction#**Linear Discriminant Analysis (LDA)**||LDA]]. It finds the linear combination of features that best separates multiple classes by maximizing the ratio of between-class variance to within-class variance. Once the optimal projection is found, it classifies new samples by projecting them onto this line and assigning them to the nearest class centroid.
###### **Support Vector Machine (SVM)**
A supervised learning algorithm that finds the optimal hyperplane that separates classes in the feature space by maximizing the margin between them. They are effective in high-dimensional spaces and are robust to overfitting, especially in cases where the number of dimensions exceeds the number of samples. It can use different kernel functions (e.g., linear, polynomial, radial basis function) to handle non-linear decision boundaries.
- **Linear SVM:** Uses a linear kernel to find a straight hyperplane that separates classes.
- **RBF SVM:** Uses a radial basis function kernel to create non-linear decision boundaries (solves the XOR problem).
###### **k-Nearest Neighbors (k-NN)**
Non-parametric (doesn't make assumptions about data distribution), instance-based method that classifies samples based on the majority class among their $k$ nearest neighbors in the feature space. Can vary in number of neighbors ($k$), distance metrics (e.g., Euclidean, Manhattan), and weighting scheme.
###### **Bayesian Classifier**
Assumes that features follow a Gaussian distribution within each class and applies [[Bayes’ Theorem||Bayes’ theorem]]  
to compute class probabilities. Its naive versions assumes feature independence given the class label, simplifying calculations, while non-naive versions don't. Its regularization parameter helps prevent overfitting by smoothing probability estimates, especially with limited data.
###### **Decision Tree Classifier**
Recursively partitions the feature space based on feature thresholds, creating a tree structure where each leaf node represents a class prediction. Hyperparameters include: maximum tree depth, minimum samples per split, and splitting criteria (e.g., Gini impurity, entropy).
###### **Random Forest Classifier**
An ensemble learning method that constructs multiple decision trees during training and outputs the mode of their predictions for classification tasks. It improves accuracy and reduces overfitting compared to individual decision trees. Hyperparameters include the number of trees, maximum tree depth, minimum samples per split, and number of features considered at each split (to add variation among trees).
###### **AdaBoost**
Sequentially trains weak classifiers (typically shallow decision trees), with each subsequent classifier focusing more on the samples misclassified by previous ones. The final prediction is a weighted combination of all weak  classifiers. Unlike Random Forest, which reduces variance, AdaBoost primarily reduces bias by iteratively improving on previous mistakes. Hyperparameters include the number of estimators (weak classifiers) and learning rate (weighting of each classifier).