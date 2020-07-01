# Dealing with matdyn’s wrong total weight problem

Matdyn will produce the wrong total weight error when the accuracies of atom position is not sufficient. Here is how to tune the program to avoid such a problem without losing too much precision.

## Definition of Problem

When running `matdyn.x`, it raises the following error:

```
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
    task #         0
    from frc_blk : error #         1
    wrong total_weight
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

Such error locates in file [`matdyn.f90`](https://github.com/QEF/q-e/blob/335abfac7c2c65b0066d19741d1a0a2b91882600/PHonon/PH/matdyn.f90#L988).

## Cause and Explaination

The subroutine [`frc_blk`](https://github.com/QEF/q-e/blob/335abfac7c2c65b0066d19741d1a0a2b91882600/PHonon/PH/matdyn.f90#L939) in `matdyn.f90` calculates the dynamical matrix at q from the force constants. It uses subroutine [`wsweight`](https://github.com/QEF/q-e/blob/7d5cebcf1250114756b88c6064ebe82e6f8fd835/PW/src/wsweight.f90#L37) to calculate whether everything should be in the WS cell is there. The `wsweight` subroutine uses a `eps` parameter to determine whether a point is on the vertex. If the atom coordinates is not accurate enough, this might be wrong.

## Steps for Resolving the Problem

1. Edit file `$QE_HOME/pw/src/wsweight.f90`, lower the value for parameter `eps`, to maybe `1.0d-4`.
2. Go to `$QE_HOME/pw/src` and run  `make libpw.a` to recompile `libpw.a`.
3. Go to `$QE_HOME/PHonon/PH` and run `make matdyn.x` to recompile `matdyn.x`

### Problem that might cause this compile unsuccessful

Some external libraries dependencies might cause compiling of this component unsuccessful. Check out `$QE_HOME/make.inc`. In my case, I removed all ELPA related items.

## Reference

1. http://www.democritos.it/pipermail/pw_forum/2012-August/024784.html
