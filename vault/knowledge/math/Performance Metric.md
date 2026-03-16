*A metric calculated from a from a confusion matrix. Often used to reflect on a [[Classifiers|classifier's]] performance.*
## Confusion Matrix
For a binary classifier, the confusion matrix is a $2\times2$ table that summarizes the performance of the classifier. It consists of four components:
- **True Positives (TP)**: The number of positive instances correctly classified as positive.
- **True Negatives (TN)**: The number of negative instances correctly classified as negative.
- **False Positives (FP)**: The number of negative instances incorrectly classified as positive.
- **False Negatives (FN)**: The number of positive instances incorrectly classified as negative.
This generalizes for multi-class classification into an $N\times N$ matrix, where $N$ is the number of classes.
## Evaluation Metrics
From the confusion matrix, several evaluation metrics can be derived:
1. **Accuracy**: The proportion of total correct predictions.$$ \text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} $$
2. **Precision**: The proportion of positive identifications that were actually correct.$$ \text{Precision} = \frac{TP}{TP + FP} $$
3. **Recall (Sensitivity)**: The proportion of actual positives that were correctly identified.$$ \text{Recall} = \frac{TP}{TP + FN} $$
4. **F1 Score**: The harmonic mean of precision and recall, providing a balance between the two metrics.$$ \text{F1 Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} $$
5. **Specificity**: The proportion of actual negatives that were correctly identified. $$ \text{Specificity} = \frac{TN}{TN + FP} $$