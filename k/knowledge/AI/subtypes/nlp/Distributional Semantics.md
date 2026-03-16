*Field of [[Natural Language Processing|NLP]] that models word meaning by analyzing their context in large text collections.*

A few important concepts:
- **Semantic Similarity:** Measures how similar two concepts are. Assessed with word similarity tests. 
- **Semantic Text Similarity (STS):** Aims at computing such similarity between larger text segments.
- **Semantic Relatedness:** How often concepts are seen together (e.g. within a 5-word window).
- **Natural Language Inference (NLI):** Task of determining the relationship between a premise and a hypothesis (entailment ($p = \text{true} \rightarrow h = \text{true}$), contradiction, neutral).
## Distributional Hypothesis 
J.R. Firth (1957): _"You shall know a word by the company it keeps"_. $\rightarrow$ This means that words that occur in the same contexts tend to convey similar meanings.
## Co-occurrence Matrix
A matrix where rows and columns represent words, and each cell contains the frequency of co-occurrence within a defined context window. 
- Used to capture semantic relationships based on context. 
- [[Distance Metric|Distance metrics]] can be used to calculate similarity.
- Not all words have the same importance; word association metrics like [[Knowledge Representation#TF-IDF (Term Frequency-Inverse Document Frequency)|TF-IDF]] and [[Knowledge Representation#PMI (Pointwise Mutual Information)|PMI]] as opposed to raw frequency can be applied to emphasize significant words.
- Serve as the basis for creating [[Embedding|word embeddings]], since dimensionality-reduction is necessary.
- **Term-Document Matrix:** A specific type of co-occurrence matrix where rows represent terms (words) and columns represent documents. Each cell contains the frequency of a term in a document (or other word association metrics). Allows the calculation of document similarity. 