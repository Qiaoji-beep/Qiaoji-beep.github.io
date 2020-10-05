---
layout: post
title: Hello!
---

For the first blog I will show some nice thing.

## Harmonic function

Harmonicity is a strong condition. Consider the Laplace's equation in the unit ball in $\mathbb{R}^2$. We put a rather wild boundary on it, say $\varphi(1, \theta) = \sin(k\theta)+1$. 
<div align="center">

$$\bigg\{
\begin{split}
&\Delta u = 0,\quad 0\leqslant r <1, \\
&u = \varphi,\quad r = 1
\end{split} $$ 

</div>
This boundary can oscillate very fast for $k$ big. However, we will see the solution is quite mild inside the ball.

### Poisson integral

The solution to the Laplace equation in the unit ball can be constructed by the so called Poisson integral,
<div align="center">

$$ u(x) = \frac{1 - |x|^2 } {n\omega_n } \int_{S^1} \frac{\varphi(y) \mathrm{d}s_y }{|x - y|^n }, \quad  x\in B. $$

</div>

The following code may take a while since it's not an efficient way to do the numerical computation. Sit down and be patient.

<div class="compute">
<script type="text/x-sage">
npi = RDF(pi)

@interact
def _(k=slider([1..10], default=3, label='Oscillation: $k$ ')):
    # Define the Poisson kernel
    P(r, theta)=(1-r^2)/(1-2*r*cos(theta)+r^2)
    # Define the boundary condition
    phi(r, t)= sin(k*t)+1
    # Compute the Poisson integral
    def u(r, theta):
        return numerical_integral(phi(r, t)*P(r, theta-t), -npi, npi)[0]/(2*npi)
    # coordinate transformation
    T = Cylindrical('height', ['radius', 'azimuth'])
    boundary = parametric_plot3d([cos(t), sin(t), phi(1, t)], (t, -npi, npi), plot_points=1000, color='red')
    show(boundary+plot3d(u, (r, 0, 1-1e-4), (theta, -npi, npi), transformation=T, plot_points=[40,1000]))
</script>
</div>

