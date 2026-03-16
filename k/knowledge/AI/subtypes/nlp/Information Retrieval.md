*Also known as IR, it is the activity of obtaining information resources automatically in large collections of unstructured text, relevant to an information need.*
## Process
1. Documents are analyzed to produce an index (inverted index: words → documents where they occur; vector store: embeddings → documents)
2. Process starts with a query (typically a list of keywords, can be a natural language question) 
3. Matching documents in the index are retrieved (documents containing the keywords or similar to the query)
- **[[Human-AI Interaction#**Retrieval-based**|Vector Space Model]]:** Uses [[Distance Metric#**Cosine Similarity**|cosine similarity]] to measure similarity between query and docs.
- **BM25:** A ranking function that considers [[Knowledge Representation#TF-IDF (Term Frequency-Inverse Document Frequency)|TF, IDF]], and average document length ($k1$ and $b$ are free parameters): $$ \text{score}(D, Q) = \sum_{q_i \in Q} IDF(q_i) \cdot \frac{f(q_i, D) \cdot (k_1 + 1)}{f(q_i, D) + k_1 \cdot (1 - b + b \cdot \frac{|D|}{avgdl})} $$