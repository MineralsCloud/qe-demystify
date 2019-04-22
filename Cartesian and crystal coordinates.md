# Cartesian and crystal coordinates

In QE, the relationship between crystal basis and Cartesian basis is
$$
\mathbf{ B }_\text{cry} = \mathbf{ B }_\text{Cart} \cdot \mathrm{ A },
$$
where $\mathrm{ A }$ is the  $3 \times 3$ matrix declared in `CELL_PARAMETERS`.

So in the reciprocal space, the relationship between reciprocal crystal coordinates and reciprocal Cartesian coordinates is
$$
\mathbf{ k }_\text{cry} \cdot \mathrm{ A }^{-1} = \mathbf{ k }_\text{Cart}.
$$
