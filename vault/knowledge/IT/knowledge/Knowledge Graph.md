*Structured representation of facts, where entities (nodes) are connected by relationships (edges).*
## KGs vs Text
- **Text Properties:** Entities, Related by structure, Implicit structure, No fixed schema, Implicit semantics, Sequential 
- **KG Properties:** Entities, Explicit relations, Explicit structure, Sometimes fixed schema, Possibly explicit semantics, Connected entities
## KG [[Embedding]]
- **Random Walk-based methods:** Extract context from each node and represent that in vector space.. Create text sequences by going from node to node, recording the nodes and relations between them. Quickly deals with large graphs and produces good embeddings. No link prediction and not totally explainable.
- **Translational embeddings / TransE:** Represent relationships as translations in vector space. For a triplet (head, relation, tail), the embedding of the tail should be close to the embedding of the head plus the embedding of the relation: $$ \text{embedding}(head) + \text{embedding}(relation) \approx \text{embedding}(tail) $$Good for predicting missing links in the graph. Worse embedding quality.
- **Graph Convolutional Networks:** Use neural networks to learn embeddings by aggregating information from neighboring nodes. Good link prediction, embedding quality, and explainability. OK training time. Requires training data and reuses embeddings less easily.