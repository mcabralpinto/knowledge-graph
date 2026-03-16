*Algorithm used to train [[Neural Network#**Feedforward Neural Network (FNN)**|FNNs]] by minimizing the loss function through gradient descent.*

Has two steps:
- **Forward Pass:** Compute the output of the network.
- **Backward Pass:** Calculate gradients of the loss with respect to weights: $$ W_{new} = W_{old} - \eta \frac{\partial f(x_{0})}{\partial x} = W_{old} - \eta \times G_{k} $$where $\eta$ is the learning rate.
## Optimizations
#### Stochastic Gradient Descent (SGD)
Updates weights using one (or a few) single training examples at a time. Much faster on large datasets, helps escape local minima due to random variation, and its frequent updates help the model converge faster on average. **Mini-batch Gradient Descent** is a compromise between SGD and Batch Gradient Descent, using small batches of data for each update.
#### Momentum 
Accelerates SGD by adding a fraction of the previous weight update to the current update, helping to smooth out oscillations and speed up convergence. $$ v_{k+1} = \beta v_{k} + (1 - \beta) G_{k} $$$$ W_{new} = W_{old} - \eta v_{k+1} $$where $v$ is the velocity (the exponentially weighted average of past gradients) and $\beta$ is the momentum term (typically between 0.9 and 0.99).
%% #### Adaptive Learning Rate 
If the loss decreases, increase the learning rate linearly; if it increases, decrease the learning rate exponentially. This helps the model converge faster but quickly corrects if it overshoots the minimum. %%
#### Adagrad
Adjusts the learning rate for each parameter based on the historical sum of squared gradients, allowing larger updates for infrequent parameters and smaller updates for frequent ones. No need to manually adjust the learning rate as it adapts itself during training. The learning rate constantly decays with the increase of iterations (the learning rate is always divided by a positive cumulative factor), therefore, the algorithm tends to converge slowly during the last iterations where it becomes very low. $$ v_{k+1} = v_{k} + G_{k}^2 $$$$ W_{new} = W_{old} - \frac{\eta}{\sqrt{v_{k}} + \epsilon} G_{k} $$where $\epsilon$ is a small constant to prevent division by zero.
#### RMSprop
Addresses Adagrad's diminishing learning rate by using a moving average of squared gradients to normalize the gradient, maintaining a more consistent learning rate throughout training. $$ v_{k+1} = \beta v_{k} + (1 - \beta) G_{k}^2 $$where $\beta$ is the decay rate (typically around 0.9).
#### ADAM (Adaptive Moment Estimation)
Combines the benefits of Momentum and RMSprop by maintaining running averages of both the gradients and their squares, allowing for adaptive learning rates for each parameter. $$m_{k+1} = \beta_{1} m_{k} + (1 - \beta_{1}) G_{k} $$$$ v_{k+1} = \beta_{2} v_{k} + (1 - \beta_{2}) G_{k}^2 $$$$ \hat{m}_{k+1} = \frac{m_{k+1}}{1 - \beta_{1}^{k+1}} $$$$ \hat{v}_{k+1} = \frac{v_{k+1}}{1 - \beta_{2}^{k+1}} $$$$ W_{new} = W_{old} - \frac{\eta}{\sqrt{\hat{v}_{k+1}} + \epsilon} \hat{m}_{k+1} $$where $\beta_{1}$ and $\beta_{2}$ are decay rates for the moment estimates (typically around 0.9 and 0.999, respectively).
## Backpropagation Through Time (BPTT)
Used to train [[Recurrent Neural Network|RNNs]] by unrolling the network across time steps and applying backpropagation to compute gradients for each time step. This allows the model to learn from sequential data and capture temporal dependencies. However, it can suffer from vanishing or exploding gradients, especially for long sequences, which is why techniques like gradient clipping and architectures like [[Recurrent Neural Network#Long-Short Term Memory (LSTM)|LSTMs]] or [[Recurrent Neural Network#Gated Recurrent Unit (GRU)|GRUs]] are often used to mitigate these issues.