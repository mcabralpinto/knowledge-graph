*Numerical representations (vectors) that capture the meaning and relationships of complex data like words, images, or audio. Based on the [[Distributional Semantics#Distributional Hypothesis|distributional hypothesis]].*
## Purpose
- Enable machines to understand and process complex data by converting it into a format suitable for mathematical operations.
- Capture semantic relationships and similarities between data points.
- Facilitate tasks like search, recommendation, and classification.
- Reduce dimensionality from methods like One-Hot Encoding (transferring words to indices in a table) while preserving context and being robust to new data.
## Text Embeddings
#### Word Embeddings
Representing words, phrases, or entities as continuous vectors in a high-dimensional space, capturing semantic relationships based on their context in large corpora. Highly flexible, but less interpretable by humans. Annotated text itself is sufficient as supervised data.
###### Static vs. Contextualized
- **Static Embeddings:** Each word has a single, fixed vector representation regardless of context (e.g., Word2Vec, GloVe, FastText). Highly limited due to multi-sense words, multi-word expressions, ...
- **Dynamic / Contextualized Embeddings:** Embedding is generated based on surrounding context; same word can have different vectors in different sentences. (e.g., ELMo, BERT, GPT). Better capture of word meaning in context, but require more computational resources.
	- Computed on-the-fly via deep models (e.g., [[Recurrent Neural Network#Long-Short Term Memory (LSTM)|LSTMs]], [[Transformer|Transformers]])
	- Incorporate syntax, position, semantics from context
	- Highly expressive and transferable across tasks
###### Word2Vec
Instead of counting the frequency of each word $w_2$ occurring near a word $w_1$, a classifier is trained for a binary decision: Is it likely to find $w_2$ near $w_1$? Learned weights are used as embedding vector.
Two approaches:
- **Continuous Bag of Words (CBoW):** Predicts a target word based on its surrounding context words.
- **Skip-gram:** Predicts surrounding context words given a target word.
###### GloVe (Global Vectors for Word Representation)
Combines global matrix factorization and local context window methods. Constructs a word-word co-occurrence matrix from the corpus, then factorizes it to obtain word vectors that capture semantic relationships - thus, captures global corpus structure and word analogies. 
Objective is to minimize the difference between the dot product of word vectors and the logarithm of their co-occurrence probability. $$J = \sum_{i,j=1}^{V} f(X_{ij}) \left( w_i^T \tilde{w}_j + b_i + \tilde{b}_j - \log(X_{ij}) \right)^2 $$Where: $$ f(x) = \begin{cases} \left( \frac{x}{x_{max}} \right)^\alpha & \text{if } x < x_{max} \\ 1 & \text{otherwise} \end{cases} $$
- $X_{ij}$: Number of times word $j$ occurs in the context of word $i$.
- $w_i$, $\tilde{w}_j$: Word vectors for the target and context words.
- $b_i$, $\tilde{b}_j$: Bias terms for the target and context words.
- $f(x)$: Weighting function to reduce the influence of very frequent co-occurrences.
**Strengths:** Strong on analogy tasks • Uses full context window • Easy to pretrain and distribute
**Limitations:** One embedding per word (not context sensitive) • Sensitive to rare-word distribution
###### FastText
Extends Word2Vec by representing each word as a sum of its subword (n-gram) vectors. This allows the model to generate embeddings for out-of-vocabulary words, improving performance on morphologically rich languages. 
**Strengths:** Handles out-of-vocabulary (OOV) and rare words, typos, and inflections effectively. 
**Limitations:** Slightly slower and bigger models than Word2Vec due to subword computations.
#### Sentence Embeddings
Representing entire sentences, paragraphs, or documents as dense vectors that capture their overall meaning and context. Can be done through:
- **Mean / Max / Mean sqrt. pooling** of word embeddings in the sentence.
- Using models that are specifically trained to generate high-quality sentence embeddings.
#### Evaluation
- **Intrinsic Evaluation:** Directly assesses the quality of embeddings using tasks like word similarity, analogy tasks, or clustering.
- **Extrinsic Evaluation:** Evaluates embeddings based on their performance in downstream tasks such as text classification, sentiment analysis, or machine translation.