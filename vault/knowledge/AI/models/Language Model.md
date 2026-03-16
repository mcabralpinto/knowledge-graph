*Complex [[Artificial Intelligence|AI]] system that learns patterns in human language to understand, generate, and predict text, allowing it to perform [[Natural Language Processing|NLP]] tasks.*
## Probabilistic LMs
- Compute the probability of a sentence / sequence of words W - $P(W) = P(w_1, ..., w_n)$
- Compute the probability of the next word - $P(w_{n+1}|w_1, ...,w_n)$
- Used for Translation, Spell Checking, Coherent Speech Recognition
#### Calculating Sentence Probability
- **Chain Rule:** $P(w_1, w_2, ..., w_n) = P(w_1) P(w_2|w_1) P(w_3|w_1, w_2) ... P(w_n|w_1, w_2, ..., w_{n-1})$, with $P(w_n|w_1, w_2, ..., w_{n-1}) = {P(w_1, w_2, ..., w_n)}/{P(w_1, w_2, ..., w_{n-1})}$. 
- CR follows Markov assumption: the probability of a word depends only on previous $n$ words 
  ($n$-gram model). Bigram example:![[Pasted image 20251231143759.png]]
#### Generating Text
With a bigram model:
- Select a random bigram `(<s>, w)`, considering its probability.
- Continue selecting bigrams based on the last word until reaching the end token `</s>.
- **Sampling:** Different types (Greedy (best sample), Random (considering probabilities), Top-$k$ (best samples), Top-$p$ (prob. threshold)). For top sampling, temperature $\tau$ controls randomness: higher $\tau$ = more random.
- **Smoothing:** Adjust probabilities to avoid zero probabilities for unseen n-grams (e.g., Laplace smoothing).
- **Evaluation:** Extrinsic (how well the model performs in a task) and Intrinsic (e.g. perplexity).
- **Perplexity:** Measure of how well a probability model predicts a sample. Lower perplexity indicates better performance. For a test set $W = w_1, w_2, ..., w_N$, perplexity is defined as: $$PP(W) = P(w_1, w_2, ..., w_N)^{-1/N} = \sqrt[N]{\prod_{i=1}^{N} \frac{1}{P(w_i|w_1, w_2, ..., w_{i-1})}}$$ Example:
   ![[Pasted image 20251231150106.png]]
- **Limitations:** Parameter number ($|V|^n$ for $n$-grams), fixed context window size, data sparsity.
## Neural LMs
- Use neural networks to learn word representations and predict next words.
- **Advantages:** Size of model does not increase with longer sequences; may consider any number of previous words; can detect long range dependencies.
- **Disadvantages:** Require large datasets and computational resources; [[Vanishing Gradient|vanishing gradient]].
###### Transformers (see [[Transformer]])