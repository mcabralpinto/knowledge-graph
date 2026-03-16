*Mathematical formula applied to a neuron's output in a [[Neural Network|neural network]] to determine whether it should "fire".*
## Types
#### Linear
A function that outputs the input directly, without any transformation. It is defined as: $$f(x) = x$$Unlike other activation functions, the linear function does not introduce non-linearity into the model, which can limit the model's ability to learn complex patterns. It is typically used in the output layer for regression problems, where the output can take any real value.
#### ReLU (Rectified Linear Unit)
A function that outputs the input directly if it is positive, otherwise it outputs zero. It is defined as:
$$f(x) = \max(0, x)$$ReLU is widely used in hidden layers of neural networks because it helps to mitigate the vanishing gradient problem, allowing for faster training and better performance. However, it can suffer from the "dying ReLU" problem, where neurons can become inactive and stop learning if they consistently receive negative inputs.
#### Leaky ReLU
A variant of ReLU that allows a small, non-zero gradient when the input is negative. It is defined as:
$$f(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha x & \text{if } x \leq 0 \end{cases}$$
where $\alpha$ is a small constant (e.g., 0.01). Leaky ReLU helps to prevent the "dying ReLU" problem by allowing a small gradient when the input is negative, which can help the model to continue learning even when some neurons receive negative inputs.
#### Sigmoid
A function that maps any input to a value between 0 and 1, often used in binary classification problems. It is defined as: $$\sigma(x) = \frac{1}{1 + e^{-x}}$$The sigmoid function is useful for modeling probabilities, as it outputs values in the range (0, 1). However, it can suffer from the vanishing gradient problem, especially for large positive or negative inputs, which can slow down training and lead to suboptimal performance.
#### Tanh (Hyperbolic Tangent)
A function that maps any input to a value between -1 and 1, often used in hidden layers of neural networks. It is defined as:$$\tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$The tanh function is similar to the sigmoid function but outputs values in the range (-1, 1), which can help to center the data and improve convergence during training. However, like the sigmoid function, it can also suffer from the vanishing gradient problem for large positive or negative inputs.