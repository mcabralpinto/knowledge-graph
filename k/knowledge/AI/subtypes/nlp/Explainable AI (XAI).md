*Exploration of methods for making AI's decisions understandable to humans.*

**Importance:** Models in AI, especially deep learning models, are often seen as "black boxes" due to their complexity, making it impossible for humans to track their decisions. Understanding them is crucial for trust, accountability, and ethical considerations in AI applications. [[Retrieval Augmented Generation|RAG]], for example, improves a model's verifiability by grounding its responses in external knowledge sources.
- **Stochastic Parrots:** Term highlighting the risk of large language models generating plausible-sounding but potentially misleading or harmful content without true understanding.
## Properties
- **Post-hoc vs. Intrinsic:** Post-hoc methods analyze already trained models, while intrinsic methods build interpretability into the model from the start.
- **Global vs. Local:** Global explanations provide insights into the overall model behavior, while local explanations focus on individual predictions.
- **Model-specific vs. Model-agnostic:** Some methods are tailored to specific model types, while others can be applied across different models.
## Methods
- **LIME (Local Interpretable Model-agnostic Explanations):** Explains individual predictions by approximating the model locally with an interpretable model. It first generates perturbed samples around the instance to be explained, annotates the original model's predictions, then fits a simple model (like linear regression) to these samples weighted by their proximity to the original instance. This simple model is then used to explain the prediction.
- **SHAP (SHapley Additive exPlanations):** Based on cooperative game theory, SHAP assigns each feature an importance value for a particular prediction. It calculates the contribution of each feature by considering all possible combinations of features and their impact on the model's output, ensuring a fair distribution of importance.