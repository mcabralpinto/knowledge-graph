*Page dedicated to ways in which humans and [[Artificial Intelligence|AI]] interact with each other.*
### Important Concepts
- [[Explainable AI (XAI)|XAI]]: Techniques that make AI decisions interpretable for humans.
### Human Roles
- **Development:** Creation of AI systems (scope, goals, architecture, algorithms, training, UI).
- **Validation:** Evaluation of AI (performance, fairness, ethics) (related to [[Reinforcement Learning|RL]]).
- **Providing Data:** Humans supply training data (annotated or unlabeled) and feedback to improve AI.
	- **Crowdsourcing:** Using large groups of people to gather data, annotations, feedback, etc.
		- **[[Kappa Agreement]]**
- **Regulation:** Establishing policies and guidelines for ethical AI use.
- **Usage:** AI as a decision-making or creative / functional partner.
### Conversational Agents
Systems designed to interact with users through natural language, either via text or speech, towards one or more goals:
- **Companion (chat-oriented):** Engage in open-ended conversations for social or emotional support.
- **Assistant (task-oriented):** Help users accomplish specific tasks (e.g. booking a flight, answering questions, *turning on the light!*).
- **Domain Expert:** Provide specialized knowledge in specific fields (e.g. medical diagnosis, legal advice).
##### Challenges
- **Speech Recognition:** Accents, background noise, etc.
	- *Language Modeling:* Computing the probability of a given sequence of words occurring in a sentence. (e. g. $P($I want to be you$) > P($I want to be U$)$?)
- **Language Variability:** Paraphrases, synonyms, idioms, etc.
- **Vagueness / Ambiguity:** Terms and phrases (e. g. *switch on the light!* $\rightarrow$ which light?).
	- *[[Knowledge Extraction#Word Sense Disambiguation (WSD)|Word Sense Disambiguation]]:* Identifying which meaning of a word is used in a given context (e. g. *bank* $\rightarrow$ financial institution or river bank?).
	- *[[Knowledge Extraction#Named Entity Recognition (NER)|Named Entity Recognition]]:* Identifying and classifying named entities (people, organizations, locations, etc.) in text, contributing to understanding its context/meaning.
- **Anaphora:** The use of an expression whose interpretation depends upon another expression in context.
	- *Coreference Resolution:* Determining when different expressions refer to the same entity in text (e. g. *Alice said she would come* $\rightarrow$ who is *she*?).
- **Ellipsis:** Omission of words that are understood in context.
### Approaches to Natural Language Understanding
###### **Keyword-based / Pattern Matching** 
Simple methods that rely on predefined keywords or patterns to extract information or respond to queries.
- **ELIZA:** A computer program that simulated conversation through “pattern matching” and substitution, that gave users an illusion of understanding, but had no built-in framework for contextualizing events.
A lexical knowledge base like WordNet can be useful for tasks like synonym expansion and word sense disambiguation.
- **WordNet:** A lexical database that groups English words into sets of synonyms (synsets), providing short definitions and usage examples, and records various semantic relations between these synonym sets. Can be used as a dictionary or as an [[Ontologies & Vocabularies|ontology]].
###### **Retrieval-based**
- **Vector Space Model:** Represents documents and queries as vectors in a multi-dimensional space (for example (?) a **term-document matrix** with counts for each word in each document of the **corpus**), allowing for the computation of similarity scores (e.g., cosine similarity) to retrieve relevant documents based on user queries.
- **[[Embedding]]:** Techniques like Word2Vec, GloVe, or BERT generate dense vector representations of words or documents that capture semantic relationships, enabling more effective retrieval of relevant information.
###### **Semantic Parsing**
Analyses the structure of a sentence and represents it as logical forms or meaning representations that can be used to query databases or knowledge graphs (e.g. Would you please feed the capybaras? $\rightarrow$ $λx~feed(x, capybaras)~[you]$). Rules can be handcrafted or learned from annotated data.
###### **Generative**
Translation of user input into a format suitable for [[Large Language Model|LLMs]] to generate responses, often augmented with retrieval from external knowledge sources to enhance accuracy and relevance. May be extended by RAG.