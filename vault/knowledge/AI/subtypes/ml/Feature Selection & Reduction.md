*Techniques that reduce a feature space, either by selecting the best ones or processing them into a smaller batch. Very common pre-processing method used in [[Machine Learning]].*
### Feature Reduction
###### **Linear Discriminant Analysis (LDA)** 
Supervised technique that finds the best [[Matrix Operations#**Linear Combination**|linear combination]] of features to separate classes by maximizing the distance between class means and minimizing the variance within each class.
It projects high-dimensional data onto a lower-dimensional space.
###### **Principal Component Analysis (PCA)**
Unsupervised technique that transforms features into a new set of uncorrelated variables called principal components, thus capturing the most variance / information in the data. 
- PCs are found by calculating eigenvectors and eigenvalues from the data's [[Covariance Matrix||covariance matrix]]. It essentially finds the axes/directions where the data spreads out the most, then projects the data onto these new axes to reduce dimensions while minimizing information loss.
### Feature Selection
###### **Kruskal-Wallis H-test**
Non-parametric (doesn't make assumptions about data distribution) statistical test used to determine if there are significant differences between the distributions of each feature. It ranks all data points from all features together and compares the sum of ranks between groups.
###### **Correlation Matrix Analysis**
Method based on building a correlation matrix to identify and remove highly correlated features. Features with high correlation (above a certain threshold) and, for each pair, the one with less correlation to the target variable is removed.
###### **Receiver Operating Characteristic (ROC) AUC Analysis**
The ROC) curve is a graphical representation of a linear classifier’s performance across different decision thresholds, plotting its sensitivity against its specificity.
This technique evaluates the performance of each feature in distinguishing between classes by calculating the Area Under the Curve (AUC) of the ROC curve. Features with higher AUC values are considered more important and are selected for the model.