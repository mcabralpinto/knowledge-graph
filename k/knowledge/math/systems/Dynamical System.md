*A type of [[System|system]] whose state is uniquely specified by a set of variables and whose behavior is described by predefined rules.*
## Concepts
#### State
- **State Variable:** A variable that describes the state of a dynamical system at a given time. The state of the system can be represented as a point in a multi-dimensional space defined by these variables
- **State Space:** The multi-dimensional space defined by the state variables of a dynamical system. Each point in this space represents a possible state of the system
- **Phase Space:** A specific type of state space that includes both the position and momentum (or velocity) of a system, often used in physics to describe the dynamics of mechanical systems
#### Dynamics
- **Seed:** The initial conditions or starting point of a dynamical system, which can influence the trajectory and long-term behavior of the system
- **Trajectory:** The path that a system's state follows through the state space over time, determined by the system's dynamics
- **Fixed Point:** A point in the state space where the system's state does not change over time, meaning that if the system starts at this point, it will remain there indefinitely. For 1D linear systems $x_{t+1} = ax_t + b$, the fixed point is $x^* = \frac{b}{1-a}$.
- **Attractor:** A fixed point towards which a dynamical system tends to evolve over time, regardless of the initial conditions (called **Stable FP**). Attractors can be points, curves, or more complex structures in the state space. **Transient** is the the trajectory between the seed and the attractor
- **Repeller:** A fixed point from which a dynamical system tends to move away over time, regardless of the initial conditions (called **Unstable FP**)
- **Saddle**: A type of equilibrium point in a dynamical system that is stable in some directions and unstable in others, meaning that trajectories can be attracted to it from certain directions while being repelled from it in others
- **Basin of Attraction:** The region of the state space that leads to a particular attractor, meaning that any initial state within this region will eventually evolve towards the attractor
## Discrete Dynamical Systems
- **Definition:** A system that evolves in discrete time steps according to a specific rule or function. The state of the system at time $t+1$ is determined by applying a function to the state at time $t$: $x_{t+1} = f(x_t)$
- **Examples:** Population growth models, cellular automata, iterative maps (e.g., logistic map), and certain types of neural networks (e.g., recurrent neural networks)
- **Advantages**:
	- no need of derivatives 
	- iteration instead of integration 
	- lower dimensionality to model abrupt changes or chaos 
	- easy to simulate on a computer 
	- sometimes best option when we have samples of system’s states at certain points in time
- Loads of examples in slide 3!
## Continuous Dynamical Systems
- **Definition:** A system that evolves continuously over time according to a set of [[Derivative#Differential Equation|differential equations]] (**see examples in slide 4a**). The state of the system at any given time is described by a vector of variables, and the rate of change of these variables is determined by a function of the current state: $\frac{dx}{dt} = f(x)$
- **Examples:** Physical systems (e.g., pendulum, planetary motion), chemical reactions, and certain types of neural networks (e.g., continuous-time recurrent neural networks)
- **Finding Fixed Points**: Set $\frac{dx}{dt} = 0$ and solve for $x$. This gives the points where the system can remain at rest (equilibrium points). The stability of these points can be analyzed using techniques like linearization and eigenvalue analysis.
#### 2D Models
###### Lotka-Volterra Model
A pair of first-order, nonlinear, differential equations used to describe the dynamics of biological systems in which two species interact, one as a predator and the other as prey. The equations are given by: $$\frac{dx}{dt} = \alpha x - \beta xy$$$$\frac{dy}{dt} = \delta xy - \gamma y$$Where:
- $x$ is the population of prey (e.g., rabbits)
- $y$ is the population of predators (e.g., foxes)
- $\alpha$ is the natural growth rate of prey in the absence of predators
- $\beta$ is the rate at which predators destroy prey
- $\delta$ is the rate at which predators increase by consuming prey
- $\gamma$ is the natural death rate of predators in the absence of prey
###### Damped Oscillation
A system that exhibits oscillatory behavior with a decreasing amplitude over time due to the presence of a damping force. The equations can be represented as: $$\frac{dx}{dt} = y$$$$\frac{dy}{dt} = -\omega^2 x - 2\zeta \omega y$$Where:
- $x$ is the position of the oscillator
- $y$ is the velocity of the oscillator
- $\omega$ is the natural frequency of the undamped system
- $\zeta$ is the damping ratio, which determines how quickly the oscillations decay
###### Van der Pol Oscillator
A nonlinear oscillator with non-conservative forces, described by the equations: $$\frac{dx}{dt} = y$$$$\frac{dy}{dt} = \mu (1 - x^2) y - x$$Where:
- $x$ is the position of the oscillator
- $y$ is the velocity of the oscillator
- $\mu$ is a scalar parameter that controls the nonlinearity and the strength of the damping. For $\mu > 0$, the system exhibits limit cycle behavior, where trajectories converge to a stable closed orbit in the phase space.
#### 3D Models
###### Lorenz Equations
A system of three coupled, nonlinear differential equations that exhibit chaotic behavior, given by: $$\frac{dx}{dt} = \sigma (y - x)$$$$\frac{dy}{dt} = x (\rho - z) - y$$$$\frac{dz}{dt} = xy - \beta z$$Where:
- $x$, $y$, and $z$ are the state variables of the system
- $\sigma$ is the Prandtl number, which represents the ratio of momentum diffusivity to thermal diffusivity
- $\rho$ is the Rayleigh number, which represents the temperature difference driving the convection
- $\beta$ is a geometric factor related to the physical dimensions of the system

The Lorenz system is famous for its chaotic solutions, which are highly sensitive to initial conditions, leading to the so-called "butterfly effect" where small changes in the initial state can result in vastly different trajectories over time. The system has a strange attractor, known as the Lorenz attractor, which is a fractal structure in the phase space that the trajectories approach but never settle into a fixed point or limit cycle. The Lorenz equations are often used as a simplified model for atmospheric convection and have been studied extensively in the field of chaos theory.
###### Rossler Attractor
A system of three coupled, nonlinear differential equations that also exhibit chaotic behavior, given by: $$\frac{dx}{dt} = -y - z$$$$\frac{dy}{dt} = x + ay$$$$\frac{dz}{dt} = b + z(x - c)$$Where:
- $x$, $y$, and $z$ are the state variables of the system
- $a$, $b$, and $c$ are parameters that control the behavior of the system. For certain values of these parameters, the system exhibits chaotic behavior, with trajectories that never settle into a fixed point or limit cycle. 

This is another example of a strange attractor, which is a fractal structure in the phase space that the trajectories approach but never settle into a fixed point or limit cycle. The Rossler system is often used as a simplified model for chemical reactions and has been studied in the field of chaos theory as well.
###### SUM-UP AT THE END OF 4B!!!