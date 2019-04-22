# Plane wave

G-vectors are generated in the `ggen` subroutine in `Modules/recvec_subs.f90`. You may also have a look at routine `PW/src/n_plane_waves.f90` to understand how things work. In general, G-vectors are determined by the condition
$$
\frac{ \hbar^2 G^2 }{ 2 m_e } \leq E_\text{cut}^\rho = 4 E_\text{cut}^\text{wf}.
$$

In `pw.x` calculation, the number of plane waves for each k-point, shown as below,

```markdown
k = 0.0714 0.2887 0.1338 (  2792 PWs)   bands (ev):
```

is dertermined by the following method.
