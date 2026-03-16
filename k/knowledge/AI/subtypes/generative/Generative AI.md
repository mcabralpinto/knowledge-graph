*Type of [[Artificial Intelligence|AI]] that generates new content, such as text, images, audio, or video, by learning patterns and structures from existing data.*
## The Generative Paradox 
The outputs produced from Generative AI are:
- New data points (not explicitly stored or directly retrieved from memory)
- Consistent with a **target domain** (valid text, plausible images, etc.).
- Derived using structural, statistical, or semantic properties (relative to rule-based, probabilistic, and meaning-aware approaches)
This means that GAI is supposed to:
- Learn patterns **without** memorizing data
- Remain coherent **without** becoming repetitive 
- Be diverse **without** losing structure 
- Be realistic **without** overfitting reality 
- Be novel **without** becoming random
## Generative vs. Discriminative Models
#### Generative Model - *"What is the probability of this data?"*
Learn data manifold $P(X|Y)$ (or $P(X)$, $P(X,Y)$). They capture underlying distribution for synthesis.
- **Data Manifold:** The shape of data distribution. Generative models learn where valid examples exist. It allows for modelling the entire data space, identifying valid/invalid regions and enabling sampling anywhere
#### Discriminative Model - *"Given input x, what is the label y?"*
Focus on learning decision boundary $P(Y|X)$. They excel at classification and regression tasks.
- **Decision Boundary:** Partition the feature space. They create regions corresponding to different classes. The focus is on class interfaces, ignoring data-sparse regions (optimized for separation).
## Paradigms
#### Symbolic
- **Production System**: Rule-based systems that generate outputs based on predefined rules and logic. Start with facts → apply matching rules → build output step by step.
- **Grammar**: Define a set of production rules that specify how to generate valid strings or structures. They can be used for language generation, procedural content creation, and more.
- **Core Logic Programming**: A paradigm where logic is expressed in terms of relations, and computation is performed through pattern matching and backtracking. It can be used for generating solutions to problems based on logical inference.
#### Evolutionary 
- Variation + Selection → Adaptation → Generation
- **Procedural Content Generation**: Use evolutionary algorithms to generate content (e.g., game levels, art) by evolving a population of candidate solutions based on a fitness function.
- IAG Slide 3 46!
- **L-Systems**: A type of formal grammar used to model the growth processes of plants and other organisms. They can generate complex structures through iterative application of production rules.
#### Statistical 
- **[[Markov Model|Markov Models]]**: Use state transitions to generate sequences based on probabilities. They can be used for text generation, music composition, and more.
	- **Extensions**: *Higher-order n-grams* (more context = more coherent output, but state space grows exponentially); *Hidden Markov Models (HMMs)* (latent states + observed emissions); *Smoothing & interpolation* (handle unseen transitions gracefully)
	- **Limitations**: *Fixed, finite memory* (can only see $n-1$ previous tokens); *No long-range dependencies* (cannot maintain coherence across paragraphs); *Exponential state growth* (higher order = exponentially more parameters); *Data sparsity* (most n-grams are never observed)
#### Connectionist 
- Markov models' limitations motivate **RNNs** (learned memory) → **LSTMs** (gated memory) → **Transformers** (attention)
- **VAEs**:
	- Explicit probabilistic model 
	- Smooth latent space 
	- Stable training 
	- Often blurrier outputs
- **GANs**:
	- Implicit generative model 
	- Adversarial training 
	- Sharp, realistic samples 
	- Unstable optimization
- **Diffusion Models**:
    - Iterative denoising process 
    - Slower generation (computationally intensive)
    - Strong quality & robustness
    - Currently dominant (SOTA in image generation)