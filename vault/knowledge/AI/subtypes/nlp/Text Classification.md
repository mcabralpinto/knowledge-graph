*The task of assigning one or more predefined categories to an input text.*
## Formal Definition
Given the input: 
- Document $d$ 
- Set of predefined classes: $C = c_1,c_2,...,c_j$ 
Text classification outputs: 
- Class $c ∈ C$, predicted for $d$
## Important Aspects

#### Document Representation (see [[Knowledge Representation]])
#### Sentiment Lexicons
- **SentiWordNet (Baccianella et al., 2010):** An extension of WordNet where each synset is associated with sentiment scores (positive, negative, objective).
- **SenticNet (Cambria et al., 2010):** A knowledge base of semantics, sentics, and polarity associated with natural language concepts.
- **AFINN (Nielsen, 2011):** A list of English words rated for valence with an integer between -5 (negative) and +5 (positive).
- **NRC VAD Lexicon (Mohammad, 2018):** A lexicon providing valence, arousal, and dominance scores for English words.
#### Challenges
- **Negation:** Handling phrases like "not good" or "never happy" that invert sentiment.
- **Comparative Opinions:** Understanding sentences that compare entities (e.g., "This phone is better than my last one.").
- **Nuanced Opinions:** Understanding subtle or mixed sentiments within a single text (e.g. "The movie had great visuals but a weak plot.").
- **Anaphora:** Resolving references to previous entities or sentiments in the text (e.g., "I loved the book. It was fantastic.").
- **Figurative Language:** Detecting when positive words are used in a negative context (e.g., "Great, another rainy day!", "Bonito serviço...").
## Rule-Based Classification
Involves creating a set of handcrafted rules or patterns to classify text:
- `If in blacklist OR ( AND ("clique" OR "querido") → Spam`
- `If ("excelente" OR "bom" OR "qualidade" OR "recomendo" ...) → +` 
- `If ("mau" OR "inaceitável" OR "sofrível" OR ... ) → -`
These rules can be based on:
- **Regular Expressions:** for example, `\d+, querid[oa]s?`
- **Linguistic Information:** for example, lemma, part-of-speech
- **Word Lists:** for example, *stopwords* related to the topic 
- **Lexicons or Knowledge Graphs**: for example, words and their typical features
## Supervised Learning
For a pre-defined set of classes $C = \{c_1, c_2, ..., c_j\}$, a labeled dataset of $m$ documents is used to train a model that can predict the class of new, unseen documents ($γ: d → c$). 
#### Generative vs. Discriminative Methods
- **Generative Models:** Learn the joint probability distribution $P(d, c)$ and use it to compute the posterior probability $P(c|d)$ for classification. Examples include [[Naive Bayes Classifier]], [[Hidden Markov Model|HMMs]].
- **Discriminative Models:** Learn the conditional probability distribution $P(c|d)$ directly, focusing on the decision boundary between classes. Examples include Logistic Regression and [[Neural Network|NNs]].
## [[Performance Metric]]