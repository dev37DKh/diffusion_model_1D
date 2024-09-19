# 1D Heat Diffusion Equation: Theory and Discretization

## Introduction
The 1D heat diffusion equation describes the transfer of heat along a 1D spatial domain (like a rod) over time. The heat equation is derived from the law of thermal conduction, which states that heat flows from regions of higher temperature to regions of lower temperature, and the conservation of energy.

## Mathematical Formulation
The 1D heat equation is a partial differential equation (PDE) given by:

$$
\frac{\partial T(x,t)}{\partial t} = \alpha \frac{\partial^2 T(x,t)}{\partial x^2}
$$

where:
- \(T(x,t)\) is the temperature at position \(x\) and time \(t\),
- \(\alpha = \frac{k}{\rho c}\) is the thermal diffusivity (with \(k\) as thermal conductivity, \(\rho\) as density, and \(c\) as specific heat capacity),
- \(\frac{\partial T(x,t)}{\partial t}\) is the rate of change of temperature over time,
- \(\frac{\partial^2 T(x,t)}{\partial x^2}\) is the second spatial derivative of temperature, representing the spatial variation of the heat flux.

### Initial and Boundary Conditions
To solve the heat equation, we need:
- **Initial Condition**: The initial temperature distribution along the rod at \(t = 0\):

  $$
  T(x, 0) = f(x)
  $$

  where \(f(x)\) is a known function.
  
- **Boundary Conditions**: Dirichlet boundary conditions are typically applied for a rod of length \(L\):

  $$
  T(0,t) = T_L \quad \text{and} \quad T(L,t) = T_R
  $$

  where \(T_L\) and \(T_R\) are fixed temperatures at the left and right ends of the rod, respectively.

## Discretization using Finite Differences
To solve the equation numerically, we discretize the space and time domains. Let the rod be divided into \(N\) grid points with spacing \(\Delta x\), and time into steps of size \(\Delta t\). The temperature at grid point \(i\) at time \(t = n\) is denoted by \(T_i^n\).

The second derivative in space can be approximated using finite differences:

$$
\frac{\partial^2 T(x,t)}{\partial x^2} \approx \frac{T_{i+1}^n - 2T_i^n + T_{i-1}^n}{\Delta x^2}
$$

Using an explicit forward time-stepping method, the time derivative is approximated by:

$$
\frac{\partial T_i^n}{\partial t} \approx \frac{T_i^{n+1} - T_i^n}{\Delta t}
$$

Combining the spatial and time discretization, we obtain the update rule for the temperature at the next time step:

$$
T_i^{n+1} = T_i^n + \alpha \frac{\Delta t}{\Delta x^2} \left( T_{i+1}^n - 2T_i^n + T_{i-1}^n \right)
$$

This equation updates the temperature at each grid point based on the temperatures at its neighbors, simulating heat diffusion over time.

## Numerical Solution Approach
To solve this numerically:
1. Initialize the temperature at each grid point based on the initial condition \(T(x,0)\).
2. Apply the boundary conditions at the endpoints \(T(0,t)\) and \(T(L,t)\).
3. Iteratively update the temperature at each time step using the finite difference scheme.

This method is implemented in Python using libraries like CasADi, Numpy, and Matplotlib for visualization.
