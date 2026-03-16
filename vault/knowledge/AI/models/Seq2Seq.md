*Also known as Sequence-to-Sequence, it is a DL model that converts an input sequence into an output sequence, commonly using an Encoder-Decoder structure with [[Recurrent Neural Network|RNNs]] or [[Transformer|Transformers]].*
## Encoder-Decoder Structure
The Seq2Seq model is divided into two primary parts linked by a "state" or "context vector".
#### The Encoder 
This component reads the input sequence sequentially. At each step $t$, it updates its hidden state $h_t$​based on the previous state and the current input token.
#### The Context Vector ($c$) 
Once the entire input is processed, the final hidden state ($h_T$​) is used to create a summary representation of the sequence. This vector must capture all necessary information for the decoder.
#### The Decoder 
The decoder generates the output tokens one by one:
- Uses $softmax$ to calculate the probability distribution for the next token in the vocabulary)
- Generation follows an [[Autoregression|autoregressive]] loop: the output from time $t−1$ becomes the input for time $t$.
- The model continues generating tokens until it outputs a special `<EOS>` token.
Its hidden state ($s_t$​) is updated using the context vector, its own previous hidden state, and the token produced in the previous step.
###### Decoding Strategies
- **Greedy Decoding:** The model simply picks the token with the highest probability at every step. While fast, it might miss a better overall sentence structure.
- **Beam Search:** Instead of one token, the model keeps the top k candidates (the "beam width") at each step. This balances quality and computational speed.
## Training 
Like standard RNNs, these models are trained using **[[Backpropagation#Backpropagation Through Time|BPTT]]** to minimize cross-entropy loss. 
#### Concepts
- **Teacher Forcing:** During training, the model is fed the "ground-truth" token from the training set as input for the next step, rather than its own (possibly wrong) prediction
- **Exposure Bias:** Refers to the mismatch between training (where the model sees correct answers) and inference (where it only sees its own potentially erroneous predictions).
- **Scheduled Sampling:** To fix exposure bias, this technique gradually replaces ground-truth tokens with the model’s own predicted tokens during the training phase.
## Limitations
- **Long Sequences:** Struggle with very long input sequences due to fixed-size context vectors.
	- **[[Attention|Attention Mechanism]]:** Introduced to allow the decoder to focus on different parts of the input sequence dynamically, improving performance on longer sequences. Instead of one summary vector, the model computes a specific context vector for every decoding step as a weighted sum of all encoder hidden states.