*Represents the instantaneous rate of change of a function with respect to its variable.*

**Definition**: The differential $dx$ of a variable quantity $x$ at any instant is the change in $x$ which would occur in the next interval of time $dt$ if $x$ were to continue to change uniformly in the interval $dt$ with the same rate which it has at the beginning of $dt$. Rate = $\frac{dx}{dt}$.
## Differential Equation
Equation where the _rate of change_ of a variable depends on the variable itself. For example, the equation $\frac{dx}{dt} = kx$ describes a situation where the rate of change of $x$ is proportional to $x$ itself, with $k$ being the constant of proportionality. This type of equation is common in modeling growth processes, such as population growth or radioactive decay.
#### Solving
###### Separation of Variables
1. Rearrange the equation to isolate the variables on different sides: $\frac{dx}{dt} = kx$ → $\frac{dx}{x} = k~dt$
2. Integrate both sides: $\int \frac{1}{x} dx = \int k~ dt$. This gives: $\ln|x| = kt + C$, where $C$ is the constant of integration
3. Solve for $x$: $x = e^{kt + C} = e^C e^{kt}$. Let $A = e^C$, so the general solution is: $x(t) = A e^{kt}$, where $A$ is determined by the initial condition (e.g., $x(0) = x_0$ gives $A = x_0$)
###### Euler's Method
1. Choose a small time step $\Delta t$ and an initial value $x(0) = x_0$
2. Use the formula: $x_{n+1} = x_n + \frac{dx}{dt} \Delta t$ to iteratively compute the next value of $x$ at each $t$
3. For the equation $\frac{dx}{dt} = kx$, this becomes: $x_{n+1} = x_n + k x_n \Delta t = x_n (1 + k \Delta t)$
4. Repeat this process to approximate the solution over time, with the accuracy improving as $\Delta t$ decreases
```python
def euler_method(k, x0, dt, steps):
    x = x0
    for _ in range(steps):
        x += k * x * dt  # Update x using the rate of change
    return x
```
###### Improved Euler's Method (Heun's Method)
This method provides a better approximation than the basic Euler's method, especially for larger time steps:
1. Compute the initial slope: $k_1 = k x_n$
2. Predict the next value using the initial slope: $x_{\text{predict}} = x_n + k_1 \Delta t$
3. Compute the slope at the predicted value: $k_2 = k x_{\text{predict}}$
4. Update the value using the average of the two slopes: $x_{n+1} = x_n + \frac{1}{2}(k_1 + k_2) \Delta t$
###### Runge-Kutta Methods
These methods provide even more accurate approximations by considering multiple intermediate slopes. The most common is the fourth-order Runge-Kutta method (RK4):
1. Compute the slopes:
   - $k_1 = k x_n$
   - $k_2 = k (x_n + \frac{1}{2} k_1 \Delta t)$
   - $k_3 = k (x_n + \frac{1}{2} k_2 \Delta t)$
   - $k_4 = k (x_n + k_3 \Delta t)$
2. Update the value using a weighted average of the slopes: $x_{n+1} = x_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4) \Delta t$