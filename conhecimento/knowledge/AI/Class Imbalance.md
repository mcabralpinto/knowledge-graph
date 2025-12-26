*Phenomenon where certain classes are misrepresented in classification task datasets. Example: HuggingFace's [```dair-ai/emotion```](https://huggingface.co/datasets/dair-ai/emotion/) dataset*
### Mitigation Strategies
- Using other [[Performance Metrics]] other than accuracy, especially focusing on per-class evaluation (per-class F1-score, precision, and recall, macro-average F1).
- Resampling - oversampling minority classes (techniques like SMOTE, be cautious of overfitting), undersampling minority classes (randomly removing examples, loses data)
- Penalizing mistakes on minority classes more heavily in the [[Loss Function]].
- Changing loss function.
- Lowering prediction threshold for minority classes.