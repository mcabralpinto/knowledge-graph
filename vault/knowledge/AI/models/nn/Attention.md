*Mechanism letting models focus selectively on important parts of input data (like words in a sentence or regions in an image) instead of treating everything equally.*

It mimics human selective focus, improving model performance by dynamically understanding relationships between data elements, often using queries, keys, and values to determine relevance. 
## How it works
Assigning weights to prioritize crucial information for better context and accuracy.
1. **Encoding**: Input data (e.g., words in a sentence) are converted into [[Embedding|embeddings]]
2. **Scoring**: The model calculates "alignment scores" between different parts, determining how relevant one piece of information (a "query") is to another (a "key").
3. **Weighting**: A $softmax$ function converts these scores into attention weights (probabilities between 0 and 1, summing to 1), highlighting important parts.
4. **Weighted Sum**: These weights are used to create a weighted sum of the "values" (the actual information), emphasizing relevant data and downplaying irrelevant data.
5. **Contextual Output**: This focused output (a contextualized representation) is then used for the next step, like generating a translation or making a prediction.