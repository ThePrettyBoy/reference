# The string method 

Consider the system modeled by 

$$
				\dot{q} = - \nabla V(q) + \xi(t),
$$

where $\xi(t)$ is the white noise. 

Assuming that the potential $V(q)$ has at least two minima $A$ and $B$.

Define the minimal energy paths, a MEP is a smooth curve connecting $A$ and $B$ which satisfies 

$$
				(\nabla V)^\top(\varphi^*) = 0,
$$

where $(\nabla V)^\top$ is the component of the $\nabla V$ normal to $\varphi^*$.

We let the $\varphi$ be a string  connecting $A$ and $B$, the simplest way to find the MEP is to evolve $\varphi$ to be 

$$
				\varphi^\perp_t  = - (\nabla V)^\perp(\varphi),
$$

with $\varphi^\perp$ being normal velocity of $\varphi$. It is obviously that the stationary solution of the above evolution equation will satisfy the minimal energy condition. For numerical purpose, it is quite convenient to have a parametized version of the above equations. Since the above equations are intrinsic, the parameterization can be arbitrarily chosen. We will mainly consider the string whihch is parametized by its normalized arc length $\alpha$ in which circurstance the evolution of the string can be reformulated as  

$$
				\begin{aligned}
				\varphi_t &= -[\nabla V(\varphi)]^\perp + \lambda \bm{\tau}  \\ 
				&=  - \nabla V(\varphi) - (\nabla V(\varphi), \bm{\tau})\bm{\tau} + \lambda \bm{\tau} \\ 
				& = - \nabla V(\varphi) + \lambda \bm{\tau}, 
				\end{aligned}
$$

where $\bm{\tau}$ represents the unit vector tagent <font color=#ff0000> to </font> the string $\varphi$, a
nd $\lambda$ is the Lagrange multiplier corresponding to the equal arc-length par
ametization of the string, which is dertermined by the following supplement const
raint of the above equations 

$$
				(|\varphi|_\alpha)_\alpha = 0.
$$

Moreover, the following boundary conditions of is given by

$$
				\varphi(0, t) = A, \ \varphi(1, t) = B.
$$

In the pracical computation, we discrete the string into $N+1$ images $\{\phi_0, \phi_1, \cdots, \phi_N\}$, with $\phi_1$ and $\phi_N$ represent the initial state and the final state. The above equation is solved by the following splitting scheme

- Evolving each image using the explicit Euler method 

$$
				\begin{aligned}
				\varphi_i^{*,k+1} &= \widetilde{\varphi}_i^{*,k} - \tau V(\varphi^k_i), \quad i  = 1,2,\cdots,N-1 \\ 
				\widetilde{\varphi}_{N}^{*,k+1} &= B.
				\end{aligned}
$$

- Redistribute the intermediate image $\widetilde{\varphi}_i^{k+1}$ along the string using the spline interpolation. To be more detailed, we first compute the normalized arc length with respect tot $\widetilde{\varphi}_i$ .
$$
				s_0 = 0, \quad s_i = s_{i-1} + |\varphi_i^* - \varphi_{i-1}^*|, \ \alpha^*_i = s_i / s_N, \ i = 1,\cdots, N.
$$
Then, we interpolae the data set $\{(\alpha_i^*, \varphi_i^{*,k+1})| i = 0, \cdots, N\}$ by cubic polynomials.


# The climbing string method 

In order to compute the transition pathways and saddle poits when the final state of a transition are unknown, the climbing string method is introduced. Similar to the classical string method, the climbing string method also evolves the string by 
$$
				\varphi_t = -\nabla V(\varphi) + \lambda\hat{\tau}.
$$
In contray to the SM, the boundary condition of CSM is modefieded to be 
$$
				\begin{aligned}
				\varphi(0,t) &= a, \\ 
				\varphi_t(1,t) &= -\nabla V(\varphi) + \nu (\nabla V(\varphi), \hat{\tau})\hat{\tau},
				\end{aligned}
$$
where $\nu$ is a prameter larger than 1. The second equation means that the potential force acting on the final point is reversed in the direction tanget to the string, which makes the final point climb uphill on the potential energy surface in this tangent direction while following the original steepest decent dynamics in the subspace perpendicular to it.

## Implementation of the climbing string method

- Evolve the string by

$$
\begin{aligned}
				\dot{\varphi}_i &= -(\nabla V)^\perp(\varphi_i), \ i = 1, \cdots, N-1 \\ 
				\dot{\varphi}_N &= -\nabla V(\varphi_N) + \nu ( \nabla V(\varphi_N), \hat{\tau}_N ) \hat{\tau}_N.
\end{aligned}
$$

The unit tanget vector $\hat{\tau}_N$ will be approximated by the following finite difference
$$
				\hat{\tau}_N = \dfrac{\varphi_N - \varphi_{N-1}}{|\varphi_N - \varphi_{N-1}|}.
$$

Integrating the above two ODE systems by the explicit Euler method reads the next is quite similar to the above, such a process is continued until convergence which is monitored according to 

$$
				\max\{\}
$$

