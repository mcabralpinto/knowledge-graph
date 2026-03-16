*Type of [[Neural Network|NN]] that have revolutionized the field of [[Natural Language Processing|NLP]] by effectively handling sequential data and capturing long-range dependencies.*

**INCOMPLETE!**

Originally proposed in the 2017 paper "Attention is All You Need" by Vaswani et al., transformers introduced a novel architecture that relies on self-attention mechanisms rather than recurrent or convolutional layers. This allows transformers to process entire sequences of data in parallel, significantly improving training efficiency and performance on various NLP tasks. 
## Key Concepts
#### Encoder-Decoder Framework
Recurrent architectures have a feedback cycle for propagating information from one step to the next, which is ideal for modelling sequential data, like text. The transformer architecture builds on this idea using an encoder-decoder framework:
- **Encoder:** Processes the input sequence and generates a set of continuous representations ([[Embedding|embeddings]]) that capture the meaning of the input.
- **Decoder:** Takes the encoder's output and generates the target sequence, one element at a time, using the previously generated elements as context. ![[Pasted image 20251231151211.png]]
- Hidden states have to include the information of all the sequence! Older information tends to get lost in the compression process...
#### Attention 
Tackles the problem above. Allows the model to weigh the importance of different words in a sequence relative to each other, enabling it to capture context and relationships effectively.
- The Encoder produces a hidden state on each step, to which the decoder may access.
- Attention prioritizes the states to use.
###### Self-Attention
Attention in all states of the same network layer, avoiding recurrence. A sequence is processed parallelly, improving efficiency in training and creating contextual embeddings.
#### Transfer Learning
Transformers are often pre-trained on large datasets (T. *body*) and then fine-tuned on specific tasks (T. *head*), allowing them to use learned representations for various specific applications.
## Popular Transformer Models
###### **BERT (Bi-directional Encoder Representations from Transformers)** 
Focuses on understanding the context of words in a sentence by considering both left and right contexts. Used for tasks like question answering and sentiment analysis. 
###### **GPT (Generative Pre-trained Transformer)** 
Primarily a decoder-based model designed for generating coherent and contextually relevant text. Used in applications like chatbots and content creation.