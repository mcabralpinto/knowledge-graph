*Mathematical formula that quantifies the difference between a [[Machine Learning|ML]] model's (ex. [[Neural Network|NNs]]) predicted output and the actual target value.*
## Types
#### Mean Squared Error (MSE)
$$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$
- Measures the **average squared difference** between predicted and actual values
- It **penalizes larger errors** more heavily, making it sensitive to outliers 
- Commonly used for **continuous-valued inputs** (e.g., images) and regression tasks
#### Binary Cross-Entropy (BCE)
$$B_{CE} = -\frac{1}{n} \sum_{i=1}^{n} [y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)]$$$$𝓛_{CE} = -\sum_{i=1}^{C} y_i \log(\hat{y}_i)$$
- Measures the **dissimilarity** between predicted probabilities and actual binary labels
- It is **sensitive to class imbalance** and can be used for binary classification tasks
- Commonly used for **binary inputs**
- The bottom formula is the generalization for multi-class classification (softmax output)