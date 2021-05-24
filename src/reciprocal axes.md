# Reciprocal axes

`pw.x` prints the reciprocal axes and k-points if you set `verbosity = 'high'`.
Be careful that the reciprocal axes and k-points in Cartesian coordinates
are not in unit "bohr⁻¹" but in unit `2pi/alat`.
For [example](https://github.com/QEF/q-e/blob/2afe9ad/PW/examples/example01/reference/al.band.ppcg.out#L64-L67):

```
     reciprocal axes: (cart. coord. in units 2 pi/alat)
               b(1) = ( -1.000000 -1.000000  1.000000 )
               b(2) = (  1.000000  1.000000  1.000000 )
               b(3) = ( -1.000000  1.000000 -1.000000 )
```

and [this one](https://github.com/QEF/q-e/blob/2afe9ad/PW/examples/example01/reference/al.band.ppcg.out#L92-L120):

```
                       cart. coord. in units 2pi/alat
        k(    1) = (   0.0000000   0.0000000   0.0000000), wk =   0.0714286
        k(    2) = (   0.0000000   0.0000000   0.1000000), wk =   0.0714286
        k(    3) = (   0.0000000   0.0000000   0.2000000), wk =   0.0714286
        k(    4) = (   0.0000000   0.0000000   0.3000000), wk =   0.0714286
        k(    5) = (   0.0000000   0.0000000   0.4000000), wk =   0.0714286
```

So if you calculate the reciprocal points using another code, you may want to time
your result with `alat/2pi`.

You may find the weights of reciprocal points add up to $2$, not $1$. According to
[this material](https://bkoz.seas.harvard.edu/files/bkoz/files/lab_2_assignment_2018.pdf),
it is an idiosyncrasy (feature) of this program. Don't worry about it.
