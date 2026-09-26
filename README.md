# 2D-nonreciprocal-Cahn-Hilliard-model

We numerically integrate the equation of motion using a pseudo-spectral method on a two-dimensional square periodic domain of side length $L$, discretized on an $N_x \times N_y$ uniform grid. In the simulations reported in the main paper, we start from random initial conditions and use $L=N_x=N_y=1024$ in the simulation shown in Fig. (1) and Fig. (3) and $L=N_x=N_y=512$ in the simulation shown in Fig. (2). To rule out finite-size effects, we also verified the robustness of these states, particularly ITC, in larger systems of size $L=N_x=N_y=2048$, without observing any qualitative changes.

To reduce aliasing errors from the pseudo-spectral evaluation of the nonlinear term, we app standard 2/3-dealiasing rule in Fourier space. Modes satisfying

$$
\left|k_x\right| \geq \frac{2}{3} k_{\max } \quad \text { or } \quad\left|k_y\right| \geq \frac{2}{3} k_{\max }
$$

are filtered out in the nonlinear update.


We use a first-order exponential time-differencing scheme, ETD1, with a fixed time step $\Delta t=0.01$, for time integration. In this scheme, the linear part of the equation is integrated implicitly in Fourier space through the exponential propagator $e^{\Delta t \mathcal{L}}$, while the nonlinear term is treated explicitly using its value evaluated from the field at the current time step. Thus, the Fourier amplitudes are updated as


$$
\phi_{\mathbf{k}}(t+\Delta t)=e^{\Delta t \mathcal{L}(\mathbf{k})} \phi_{\mathbf{k}}(t)+\Delta t \varphi_1(\Delta t \mathcal{L}(\mathbf{k})) \mathcal{N}_{\mathbf{k}}(t),
$$

Where $\varphi_1(z) =(e^z-1)/z $. The ETD formulation improves numerical stability by exactly resolving the linear growth while retaining an explicit pseudo-spectral evaluation of the nonlinear contribution.
