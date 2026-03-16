*Type of [[Neural Network|NN]] used in unsupervised learning to learn efficient encodings for data by training the network to copy its input to the output.*
## Basics
The main idea of an Autoencoder is that it compresses input data into a low-dimensional [[Latent Space|latent space]] representation (encoding) and then reconstructs the output (decoding) to minimize reconstruction error. The learned representation is:
- **Brittle**: Small changes in the latent space may produce invalid outputs
- **Discontinuous**: Changes in the latent space provoke abrupt changes in the output
- **Unstructured**: No explicit organization or semantics in the latent space
#### Architecture
![[Pasted image 20260308100916.png]]
- **Encoder**: Maps input data to a latent space representation (bottleneck layer). It learns to capture the most salient features while reducing dimensionality. $f :x↦z=σ(Wx+b)$
- **Bottleneck Layer**: The layer in the middle of the network with fewer neurons than the input/output layers. It forces the network to learn a compressed representation of the data, capturing essential features while discarding noise and redundancy.
- **Decoder**: Maps the latent representation back to the original input space, reconstructing the data. It learns to generate outputs that resemble the original inputs. $g:z↦ \hat{x}= σ(Wz+ b')$
- **[[Loss Function]]**: The network is trained to minimize the difference between the input and output, often using Mean Squared Error (MSE) or Binary Cross-Entropy (BCE) depending on the data type.
#### Training
1. **Forward Pass**: encode $x \rightarrow z$ decode $z \rightarrow x̂$ 
2. Compute reconstruction loss $L(x, x̂)$
3. Backpropagate gradients through encoder and decoder jointly
4. Update all parameters $θ_{enc}$, $θ_{dec}$ via [[Backpropagation#Optimizations|gradient descent]] (Adam, SGD+momentum)
5. Repeat for all mini-batches until convergence
#### Undercomplete vs. Overcomplete
- **Undercomplete Autoencoder**: The bottleneck layer has fewer neurons than the input layer, forcing the network to learn a compressed representation. It is effective for dimensionality reduction and feature learning.
- **Overcomplete Autoencoder**: The bottleneck layer has more neurons than the input layer, allowing the network to learn a more complex representation. However, it may lead to overfitting and simply copying the input without learning meaningful features. [[Regularization]] techniques (e.g., sparsity constraints, denoising) are often used to prevent this.
## Classical Autoencoders
#### Denoising Autoencoder (DAE)
Trained to reconstruct clean inputs from noisy versions, encouraging the model to learn robust features that capture the underlying structure of the data rather than memorizing specific examples. Goal is to minimize loss against clean version. ![[Pasted image 20260308103839.png]]
#### Sparse Autoencoder
Instead of limiting how many neurons exist, you limit how many neurons fire at once. This sparsity is encouraged in the latent representation by adding a regularization term to the loss function that penalizes non-zero activations in the bottleneck layer. This forces the network to learn a more efficient and interpretable representation of the data, where only a few neurons are active for any given input.
#### Contractive Autoencoder (CAE)
Penalize the encoder for being too sensitive to small changes in the input. This is achieved by adding a regularization term to the loss function that encourages the encoder to learn a representation that is robust to small perturbations in the input data. The Jacobian penalty effectively creates an "information bottleneck" without reducing dimensionality, forcing most directions in the latent space to be insensitive to input changes, so only a few directions carry meaningful information.
$$𝓛=𝓛_{recon}(x,\hat{x})+λ~⋅∥J_{f}(x)∥_{F}^2$$
$J_{f}(x) = \frac{∂f(x)}{∂x}$ is the Jacobian matrix of the encoder function $f$ with respect to the input $x$, and $∥J_{f}(x)∥_{F}^2=\sum_{i,j} \left( \frac{∂f_i(x)}{∂x_j} \right)^2$ is the squared Frobenius norm of this Jacobian, which measures how much the encoder's output changes in response to small changes in the input. By minimizing this term, the contractive autoencoder encourages the encoder to learn a representation that is robust to small perturbations in the input data, leading to a more stable and meaningful latent representation.
#### Limitations
- **Discontinuous Latent Space**: Points between two encoded training examples don't necessarily decode to meaningful outputs. The encoder doesn't guarantee a smooth, structured latent manifold. 
  **No Generative Prior**: There is no defined distribution over the latent space. We can't sample $z \sim p(z)$ and expect to decode a realistic sample. The latent space is not regularized. 
- **No Interpolation Guarantee**: Encoder may map very different inputs to the same latent code, and small variations in latent space produce wildly different outputs.
- **Latent Space Holes**: Linear interpolation between two latent codes may pass through *holes*, regions of latent space that decode to garbage. Not suitable for creative generation. 
## Convolutional Autoencoder (CAE)
Designed for image data, they use convolutional layers in the encoder and decoder to capture spatial hierarchies and local patterns. The encoder consists of convolutional and pooling layers that reduce the spatial dimensions while increasing the number of feature maps, creating a compact latent representation. The decoder uses up-sampling and convolutional layers to reconstruct the original image from the latent representation. This architecture is effective for tasks like image denoising, inpainting, and dimensionality reduction while preserving spatial information.
#### Decoder Approaches
- **Transposed Convolution**: Also known as deconvolution, it uses learned filters to up-sample the feature maps, allowing the network to learn how to reconstruct spatial details effectively.
- **Up-sampling + Convolution**: First, the feature maps are up-sampled using techniques like nearest neighbor or bilinear interpolation, and then a convolutional layer is applied to refine the output. This approach can be computationally more efficient and can help reduce checkerboard artifacts that sometimes occur with transposed convolutions.
#### U-Net Architecture
**Skip Connections** concatenate encoder feature maps to decoder inputs at each level. This allows the decoder to recover fine-grained spatial detail lost during pooling, which is crucial for dense prediction tasks (segmentation, inpainting).![[Pasted image 20260308111811.png]]
## Variational Autoencoder (VAE)
VAEs introduce a probabilistic framework to the autoencoder architecture, allowing for a continuous and structured latent space. Instead of encoding an input into a single point in the latent space, the encoder maps the input to a distribution (typically Gaussian) characterized by a mean and variance. During training, the model samples from this distribution to obtain a latent code, which is then passed through the decoder to reconstruct the input. 
![[Pasted image 20260308112302.png]]
...