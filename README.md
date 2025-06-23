# Continuum model for an epithelial tissue
Calculation of flow field and stresses in a model for epithelial tissue with active mechano-chemical feedback.

The fundamental quantity of the model is the time varying anisotropic spatial distribution of actomyosin within cells, quantified by the 2nd rank tensor $\mathbf{M}({\bf{r}},t)$. 
The other fields that characterise the material are local velocity ${\bf{v}}({\bf{r}}, t)$ and the local passive stress $\bm{\pi}({\bf{r}}, t)$. The total stress $\bm{\sigma}({\bf{r}}, t)$ in the material is the sum of the passive stress and an active stress proportional to $\bm{M}$ : $\bm{\sigma} = \bm{\pi} + \beta(\bm{M} - m_0\bm{I})$, where $\beta$ is the activity parameter and $m_0$ is the reference concentration for actomyosin. The actomyosin tensor evolves via
```math
\tau_m\overset{\circ}{\mathbf{M}} = \mathbf{I} - (\mathbf{I} + e^{-k_0\mathbf{\sigma}})\cdot\mathbf{M} + D\nabla^2\mathbf{M},
```
where the over circle represents the corotational derivative $\accentset{\circ}{\bm{A}} = \partial_{t}\bm{A} + {\bf{v}}\cdot\nabla \bm{A} + \bm{\omega}\cdot\bm{A} - \bm{A}\cdot\bm{\omega}$, where $\bm{\omega} = (1/2)(\nabla {\bf{v}} - (\nabla {\bf{v}})^T)$ is the vorticity tensor. We also include ActoMyosin diffusion with diffusion constant $D$. We use a convected compressible Maxwell model for the passive stress, superimposing separate Maxwell models for compression and shear deformations, 
```math
\boldsymbol{\pi} + \tau_v\accentset{\circ}{\bm{\pi}} = \frac{1}{2}\eta_p\text{Tr}(\dot{\bm{\gamma}})\bm{I}  + \eta_s\left(\dot{\bm{\gamma}} - \frac{1}{2}\text{Tr}(\dot{\bm{\gamma}})\bm{I}\right),
```
where $\tau_v$ is the viscous relaxation time scale, $\eta_p$ is the bulk viscosity, $\eta_s$ is the shear viscosity, and the strain rate tensor is related to the velocity field via $\dot{\bm{\gamma}} =  (1/2)(\nabla {\bf{v}} + (\nabla {\bf{v}})^T)$. The bulk and shear moduli of the system are related to the relaxation time scale and the viscosities via $\tau_v = \eta_p /B = \eta_s/\mu$. The tissue is coupled to a substrate with friction coefficient $\zeta$ via momentum balance in the over-damped limit,
```math
\zeta{\bf{v}} = \nabla\cdot\bm{\sigma}.
````
More details can be found in our [paper](https://doi.org/10.1103/PhysRevLett.131.238301)[^1]

![GIF](https://github.com/aondoyima/mechano-chemical-model/blob/main/mov_oscstate_6x6.gif)

[^1]: Ioratim-Uba, A., Liverpool, T. B., & Henkes, S. (2023). Mechanochemical active feedback generates convergence extension in epithelial tissue. Physical Review Letters, 131(23), 238301.

## How to use
- Input parameters and run the simulation using ```bash run_batch.sh```. 
- "main.py" carries out the numerical solution for the coupled differential equations in the model for the actomyosin tensor, passive pressure, and velocity field.
- You can generate a movie of the simulation with "make_movie.py". The function "utils.plot_fields()" takes optional arguments - see comments in "make_movie.py"

## Dependencies and Packages
Outside of the packages in the standard python library, you will need these:
- [ffmpeg](https://ffmpeg.org/) for turning a series of plots into a movie
- [Matplotlib](https://matplotlib.org/) is a comprehensive library for creating static, animated, and interactive visualizations in Python.
- [NumPy](https://numpy.org/) is the standard package for scientific computing with Python
