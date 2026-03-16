*Also known as RNN, it is a type of [[Neural Network|NN]] designed for sequential data, such as time series or natural language.

In its simplest architecture, it maintains a hidden state that captures information from previous inputs, allowing it to model temporal dependencies. Commonly used in language modeling and speech recognition. Architecture includes:
- **Input Layer:** Receives sequential data.
- **Recurrent Layers:** Process sequences by maintaining a hidden state that captures information from previous time steps.
- **Output Layer:** Produces predictions based on the processed sequence.
Trained through [[Backpropagation#Backpropagation Through Time (BPTT)|BPTT]], which unrolls the network across time steps to compute gradients and update weights.
## Long-Short Term Memory (LSTM)
A type of RNN designed to address the vanishing gradient problem, allowing it to capture long-term dependencies in sequential data. LSTMs use a gating mechanism to control the flow of information, enabling them to retain or forget information as needed. 
## Gated Recurrent Unit (GRU)
A simplified version of LSTM that also addresses the vanishing gradient problem. GRUs combine the forget and input gates into a single update gate, reducing the number of parameters while still effectively capturing long-term dependencies in sequential data.