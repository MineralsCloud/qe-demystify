# Cartesian and crystal coordinates

In QE, the relationship between crystal basis and Cartesian basis is
$$
\mathbf{ B }_\text{cry} = \mathbf{ B }_\text{Cart} \cdot \mathrm{ A },
$$
where $\mathrm{ A }$ is the  $3 \times 3$ matrix declared in `CELL_PARAMETERS`.
$$
\mathrm{ A } = \begin{pmatrix}
  — \mathbf{ v }_1 —  \\
  — \mathbf{ v }_2 — \\
  — \mathbf{ v }_3 —
\end{pmatrix}.
$$
So in the reciprocal space, the relationship between reciprocal crystal coordinates and reciprocal Cartesian coordinates is
$$
\mathbf{ k }_\text{cry} \cdot \mathrm{ A }^{-1} = \mathbf{ k }_\text{Cart}.
$$

## The output of `matdyn.x`

The output of `matdyn.x` is in Cartesian coordinates, even if you specify

```fortran
q_in_cryst_coord = .true.
```

in the input.

For example, for a BCC crystal, the `CELL_PARAMETERS` will be
$$
\mathrm{ A } = \begin{pmatrix}
  0.5 & 0.5 & 0.5\\
 -0.5 & 0.5 & 0.5\\
 -0.5 & -0.5 & 0.5
\end{pmatrix},
$$
so $1/ 4 \begin{bmatrix} 1 & 1 & 1 \end{bmatrix}$ in crystal coordinates will be
$$
1 / 4 \thinspace \mathrm{ A }^{-1} \cdot \begin{bmatrix} 1\\ 1\\ 1 \end{bmatrix} = \begin{bmatrix}
	0\\
	0\\
	1/2
\end{bmatrix}.
$$
