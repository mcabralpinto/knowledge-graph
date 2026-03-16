*[[Machine Learning|ML]] model inspired by the human brain. Consists of interconnected layers of operational nodes that simulate neurons, allowing it analyze data and learn patterns.*

Consists of:
- **Input Layer:** Receives raw data and passes it to the next layer.
- **Hidden Layers:** Perform computations and extract features through weighted connections.
- **Output Layer:** Produces the final result, such as classification or prediction.
Each layer has a set number of artificial neurons.
Related to [[Loss Function]] and [[Activation Function]].
## Types

#### **Feedforward Neural Network (FNN)**
Simplest type of NN where information moves in one direction, from input to output, without cycles. Used for basic classification and regression tasks. Architecture includes:
- **Input Layer:** Receives input features.
- **Hidden Layers:** One or more layers that process inputs using weighted connections and activation functions.
- **Output Layer:** Produces final predictions.
Trained using [[Backpropagation|backpropagation]] to minimize a loss function by adjusting weights based on the error of predictions.
#### **Convolutional Neural Network (CNN)**
Specialized for processing grid-like data, such as images. Uses convolutional layers to automatically and adaptively learn spatial hierarchies of features from input images. Commonly used in image recognition and computer vision tasks. Usually has the following architecture:
- **Convolutional Layers:** Apply filters to the input to create feature maps.
- **Pooling Layers:** Reduce the spatial dimensions of feature maps, retaining important information.
- **Flattening Layer:** Converts the pooled feature maps into a one-dimensional vector.
- **Fully Connected Layers:** Perform high-level reasoning and produce the final output.
#### **Graph Neural Networks (GNNs)**
Designed to work with graph-structured data, such as social networks or molecular structures. GNNs capture relationships between nodes (entities) and edges (connections) to perform tasks like node classification, link prediction, and graph generation. They typically consist of:
- **Input Layer:** Represents the graph structure and node features.
- **Graph Convolutional Layers:** Aggregate information from neighboring nodes to learn node representations.
- **Output Layer:** Produces predictions based on the learned node representations, such as classifying nodes or predicting links between nodes.
#### [[Recurrent Neural Network|Recurrent Neural Network (RNN)]]

