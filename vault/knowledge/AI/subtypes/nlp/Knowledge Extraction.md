*The process of automatically finding, capturing, and structuring valuable information from vast amounts of raw data (both structured and unstructured) to create machine-readable knowledge.*
## Text Extraction
It is the act of extracting structured information from unstructured or semi-structured data sources, such as text documents. An essential first step in building knowledge-based systems.
- **Information Extraction** aims at extracting structured information from (unstructured) natural language text (vocabulary, entities, relations, time, events, ...). 
- **Knowledge Extraction** extends this to representing the extracted info as knowledge structures.
#### Tokenization
The process of breaking down text into smaller units called tokens (words, phrases, symbols, or other meaningful elements). Tokenization is a crucial step in [[Natural Language Processing|NLP]] as it prepares the text for further analysis and processing.
###### Term Extraction 
Identifying and extracting relevant terms or keywords from the text that represent important concepts or entities within a specific domain (e.g. through TF-IDF or PMI).
- **TF-IDF (Term Frequency-Inverse Document Frequency):** Statistical measure that evaluates the importance of a word in a document relative to a collection of documents (corpus). It is calculated as: $$ \text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t) $$where $TF(t, d)$ is the frequency of term $t$ in document $d$, and $IDF(t) = \log\left(\frac{N}{DF(t)}\right)$, with $N$ being the total number of documents and $DF(t)$ the number of documents containing term $t$.
	- **Stopwords:** Common words (e.g., "the", "is", "in") that are often filtered out by IDF, as their high frequency across documents makes them less informative.
- **PMI (Pointwise Mutual Information):** Measures the association between two events (e.g., words) by comparing their joint probability to the probabilities of them occurring independently. It is calculated as: $$ \text{PMI}(x, y) = \log\left(\frac{P(x, y)}{P(x) \times P(y)}\right) $$ A higher PMI indicates a stronger association between the events.
###### Part-of-Speech (PoS) Tagging
Assigns grammatical categories (nouns, verbs, adjectives, etc.) to each token in a text based on its context and definition. PoS tagging is essential for understanding the syntactic structure of sentences and is often used as a preprocessing step in NLP tasks.
###### Named Entity Recognition (NER)
Identifies and classifies named entities (people, organizations, locations, dates, etc.) in text into predefined categories. NER is commonly used in NLP tasks to extract structured information from unstructured text.
#### Sequence Labelling
Assigns labels $L = \{N,V,D,\dots\}$ to each token $w=\{w_1,...,w_n\}$ in a sequence, often used for tasks like PoS tagging and NER. It helps understand the structure and meaning of text by providing annotations specific to context.
- **For PoS tagging:** Uses probabilistic models (e.g., [[Hidden Markov Model|HMMs]]) to predict the most likely sequence of labels based on observed tokens.
- **For NER:** Delimitation of text chunks that correspond to named entities, often using BIO (Beginning, Inside, Outside) notation to indicate entity boundaries.
- [[Conditional Random Field|CRFs]], [[Recurrent Neural Network|RNNs]], and [[Transformer|Transformers]] are commonly used models for sequence labelling tasks.
#### Relation Extraction
Aims at obtaining the relationships between the extracted terms and entities.
###### Pattern-based
Uses predefined linguistic patterns or rules to identify relationships between entities in text. These patterns can be based on syntactic structures, keywords, or specific phrases that indicate a relationship.
###### Supervised
0. Define relation types to extract and annotate them in a collection 
1. Identify pairs of entities in the same sentence, $e_1$ and $e_2$ 
2. Train binary classifier for deciding whether $e_1$ and $e_2$ are related. 
	- Positive examples: pairs of related entities 
	- Negative examples: pairs of entities that, even if in the same sentence, are not related 
3. Train classifier for assigning relation type to pairs of related entities (many useful features: PoS tags, words around entities, etc.)
###### Distant Supervision
1. Use existing knowledge base (KB) to obtain pairs of related entities
2. Find sentences containing those entity pairs and assume they express the relation from the KB
3. Use resulting corpus for supervised relation extraction
###### Open Information Extraction (OIE)
Extract relation instances without relying on token-level patterns or requiring any relation specific training data. It instead relies on PoS-tags, chunks, syntactic dependencies, etc. to identify potential relations and their arguments in text.
###### Relation Ontologization
Associating relation phrases with an ontological representation, i.e., a relation defined in the [[Knowledge Graph|knowledge graph]] / [[Ontologies & Vocabularies|ontology]]. Possible steps include:
- Normalizing the relation phrase (e.g., "is the capital of" → "capitalOf")
- Mapping the normalized phrase to an existing relation in the ontology
- Finding relations that share the same domain and range as the extracted relation
#### Word Sense Disambiguation (WSD)
The process of determining the correct meaning (sense) of a word in a given context when the word has multiple meanings. WSD is crucial for accurate understanding and interpretation of text.
There are several approaches:
- **Supervised:** requires much training data (large dictionaries, several occurrences of different word senses in context, ...) 
	- **[[Bayes’ Theorem|Bayesian]]:** $P(s_i|C) = \alpha P(s_i) \prod_{w_j \in C} P(w_j|s_i)$ where $s_i$ is a word sense and $C$ is the context
- **Knowledge-based:** Word + context → Word sense
	- **Lesk Algorithm:** Selects the sense whose definition shares the most words with the context.
- **[[Embedding]]:** Contextual embedding → sense embedding \[Wiedemann et al., 2019]
###### Lemmatization
The process of reducing words to their base or root form (lemma) by considering the context and morphological analysis. Unlike stemming, which simply trims word endings, lemmatization ensures that the resulting lemma is a valid word in the language.
#### Entity Linking
Task of automatically identifying named entities mentioned in text and connecting them to an entry in a knowledge base. Mix of NER and WSD.