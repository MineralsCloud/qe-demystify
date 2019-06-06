# `wsweight` function

This function is defined in `PW/src/wsweight.f90` file.

`wsweight` assigns this weight:

- if a point is inside the Wigner-Seitz (WS) cell: weight $w = 1$.
- if a point is outside the WS cell: weight $w = 0$.
- if a point $\mathbf{ q }$ is on the border of the WS cell, it finds the number $N$ of translationally equivalent point $\mathbf{ q } + \mathbf{ G }$ (where $\mathbf{ G }$ is a lattice vector) that are also on the border of the cell. Then weight $w = 1/N$.

That is, if a point is on the surface of the WS cell of a cubic lattice it will have weight $1/2$; on the vertex of the WS it would be $1/8$; the $\mathbf{ K }$ point of an hexagonal lattice has weight $1/3$ and so on.

It takes $3$ parameters, as shown below,

```fortran
function wsweight(r,rws,nrws)
```

where

- `r` means a real space vector, a `real` vector of length `3`;
- `rws` means Wigner-Seitz real space vectors, a `real` matrix of size `(0:3, nrws)`;
- `nrws` means the number of Wigner-Seitz real space vectors, an `integer`.

rws(0:3,nrwsx)   *! nearest neighbor list, rws(0,\*) = norm^2*

*number of nearest neighbor*