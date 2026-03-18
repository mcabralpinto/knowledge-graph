*Set of metrics that determine closeness/distance between different data points.*
## Vector Similarity
#### **Euclidean**
Straight-line distance between two points in n-dimensional space. Sensitive to magnitude differences. $$d(p, q) = \sqrt{\sum_{i=1}^{n} (p_i - q_i)^2}$$
#### **Manhattan** 
Sum of absolute differences between coordinates of two points. Useful for high-dimensional spaces because it reduces the impact of outliers.
$$d(p, q) = \sum_{i=1}^{n} |p_i - q_i|$$
#### **Cosine Similarity** 
Measures the cosine of the angle between two non-zero vectors. Focuses on orientation rather than magnitude, making it useful for text analysis.
$$\text{similarity}(A, B) = \frac{A \cdot B}{||A|| \times ||B||} = \frac{\sum_{i=1}^{n} A_i B_i}{\sqrt{\sum_{i=1}^{n} A_i^2} \times \sqrt{\sum_{i=1}^{n} B_i^2}}$$
