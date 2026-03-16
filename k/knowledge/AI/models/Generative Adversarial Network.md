*Also known as GAN, it is a ML framework where two neural networks (Generator/Discriminator) compete against each other to create realistic, synthetic data from a training set.*
## Motivation
Coming from the limitations of traditional generative models (e.g., VAEs) that often produce blurry outputs, GANs were introduced to generate sharper, more realistic samples by learning an implicit model of the data distribution through adversarial training.
- Optimization of per-pixel accuracy $\rightarrow$ Optimization for fooling a critic
- Rewarding average of plausible outputs $\rightarrow$ Rewarding samples that look real
- Averaging (blur) $\rightarrow$ The discriminator penalizes blurry, unrealistic outputs directly (pushes samples toward realism, sharpness)
- Safe but perceptually unsatisfying $\rightarrow$ Risky but perceptually convincing
## Idea
We introduce two models that compete against each other:

- **Generator $G(z)$**: A model that takes random input (noise) and attempts to create data that resembles the training set (e.g., generating a fake image).
	- **Latent Variable $z$**: A random input (often sampled from a simple distribution like Gaussian) that the generator uses to produce synthetic data. It captures the underlying structure of the data distribution.
- **Discriminator $D(x)$**: A model that evaluates data, trying to distinguish between genuine data from the training set and "fake" data created by the generator.

The two networks are trained simultaneously. The generator tries to minimize the chance that the discriminator detects its fakes, while the discriminator tries to maximize its detection accuracy.
## Objective
The training process can be formalized as a minimax game with the following objective function:
$$\min_G \max_D V(D, G) = \mathbb{E}_{x \sim p_{data}(x)}[\log D(x)] + \mathbb{E}_{z \sim p_z(z)}[\log(1 - D(G(z)))]$$
Where $x \sim p_{data}(x)$ represents real data samples and $z \sim p_z(z)$ represents random noise input to the generator. 

- Discriminator aims to maximize $V$, the probability of correctly classifying real and fake data
	- $D(x)→1$ for real images  
	- $D(G(z))→0$ for fake images
- Generator aims to minimize $V$, the probability that the discriminator correctly identifies its outputs as fake
	- $D(G(z))→1$ for fake images (fooling the discriminator)
#### In Practice...
The minimax objective is elegant, but for implementation purposes we we split it into two separate updates, and then the generator's loss reveals a critical flaw.
- **$G$ minimizes $log(1−D(G(z)))$**: When $D$ is confident, gradients vanish, meaning $G$ gets no useful learning signal early on 
- **$G$ maximizes $log(D(G(z)))$**: This non-saturating heuristic provides stronger gradients when the generator is performing poorly, leading to more stable training and faster convergence.
#### Optimal Discriminator
Given a fixed generator, the optimal discriminator can be derived as:
$$D^*(x) = \frac{p_{data}(x)}{p_{data}(x) + p_g(x)}$$
Where $p_{data}(x)$ is the probability distribution of the real data and $p_g(x)$ is the probability distribution of the generated data. This means that the optimal discriminator outputs the probability that a given sample is real based on the relative likelihood of it being generated versus being from the real data distribution.

- If $G$ is perfect ($p_g = p_{data}$), then $D^*(x) = 0.5$ for all $x$, meaning the discriminator cannot distinguish between real and fake data.
- If $G$ is bad, then $D^*(x) \approx 1$ for real data and $D^*(x) \approx 0$ for generated data, indicating that the discriminator can easily tell them apart.

Substituting $D*$ into the GAN objective shows that training $G$ minimizes a quantity related to the [[Divergence#Jensen-Shannon Divergence (JS Divergence)|JS divergence]] between $p_g$ and $p_{data}$, which encourages the generator to produce data that closely matches the real data distribution. (+)
## Training
1. Sample a minibatch of real data
2. Sample a minibatch noise vectors $z$
3. Generate fake data using the generator: $G(z)$
4. Update $D$ by maximizing the log-likelihood of correctly classifying real and fake data
5. Sample fresh noise vectors $z$
6. Update $G$ by minimizing the log-likelihood of the discriminator correctly identifying generated data
7. Repeat until convergence (or for a fixed number of iterations)
#### Challenges
- **Mode Collapse**: The generator produces limited varieties of outputs, failing to capture the full diversity of the data distribution. It can be mitigated by techniques like minibatch discrimination, unrolled GANs, or using different architectures. (+)
- **Vanishing Gradients**: If the discriminator becomes too strong, the generator receives very weak gradients, making it difficult to learn. This can be addressed by using the non-saturating heuristic for the generator's loss or by balancing the training of both networks.
- **Oscillations**: The training process can become unstable, with the generator and discriminator failing to converge. Techniques like feature matching, adding noise to the inputs of the discriminator, or using different architectures can help stabilize training.
## Variants
#### Deep Convolutional GAN (DCGAN)
Uses the following design rules:
- **Replace all pooling with strided convolutions**, to allow the model to learn its own spatial down-sampling and up-sampling. 
- Use **batch normalization in both $G$ and $D$**, because it helps to stabilize training by normalizing the inputs to each layer, which can reduce internal covariate shift and allow for higher learning rates. It also helps to prevent [[Generative Adversarial Network#Training|mode collapse]] by adding noise to the activations, which encourages the generator to produce more diverse outputs.
- **Remove fully connected layers**, because they can lead to overfitting and are not necessary for learning spatial hierarchies in images. Instead, the architecture relies on convolutional layers to capture spatial features effectively. 
- **ReLU [[Activation Function|activation]] in $G$ (except Tanh for output)**, because it allows for better gradient flow and helps to avoid vanishing gradients, while also promoting sparsity in the activations, which can lead to more efficient learning.
- **LeakyReLU activation in $D$**, because it allows a small, non-zero gradient when the input is negative, which helps to prevent the "dying ReLU" problem where neurons can become inactive and stop learning. This is particularly important in the discriminator, which needs to learn from both real and fake samples effectively.
- Use transposed convolutions for up-sampling in $G$, because they allow the model to learn how to up-sample the feature maps in a way that can capture complex spatial relationships, leading to sharper and more realistic generated images.
#### Conditional GAN (cGAN)
Extends the GAN framework by conditioning both the generator and discriminator on additional information $y$ (e.g., class labels, text descriptions). The objective function is modified to:
$$\min_G \max_D V(D, G) = \mathbb{E}_{x \sim p_{data}(x)}[\log D(x|y)] + \mathbb{E}_{z \sim p_z(z)}[\log(1 - D(G(z|y)))]$$
This allows the generator to produce outputs that are not only realistic but also aligned with the specified conditions, enabling tasks like class-conditional image generation or text-to-image synthesis. The discriminator also learns to evaluate the authenticity of the generated data in the context of the given conditions, improving the overall quality and relevance of the generated samples.
#### Wasserstein GAN (WGAN)
Addresses the issue of vanishing gradients and mode collapse by using the [[Divergence#Wasserstein Distance (Earth Mover's Distance)|Wasserstein distance]] instead of the [[Divergence#Jensen-Shannon Divergence (JS Divergence)|JS divergence]]. The objective function is modified to:
$$\min_G \max_D V(D, G) = \mathbb{E}_{x \sim p_{data}(x)}[D(x)] - \mathbb{E}_{z \sim p_z(z)}[D(G(z))]$$
Where $D$ is now a critic that outputs real-valued scores instead of probabilities. The WGAN framework also includes a gradient penalty term to enforce the Lipschitz constraint on the critic, which helps to stabilize training and improve convergence. This results in a more stable training process and better quality of generated samples, as the generator receives meaningful gradients even when the critic is performing well, allowing it to continue improving over time.
- **Lipschitz Constraint**: A condition that requires the critic function to have a bounded gradient, ensuring that small changes in the input lead to small changes in the output. This is typically enforced using a gradient penalty term in the WGAN objective, which helps to stabilize training and prevent issues like mode collapse.
#### Bidirectional GAN (BiGAN)
#### StyleGAN

## Evaluation

