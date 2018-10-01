# Force constant

[TOC]

## QE 6.3

### Header

In Quantum ESPRESSO’s `PHonon/examples` , there is an example `alas.444.fc` for showing the force constant output. All the following information are written in `/path/to/qe-6.3/PHonon/PH/matdyn.f90`.

The first line,

```
  2    2  2 10.5000000  0.0000000  0.0000000  0.0000000  0.0000000  0.0000000
```

where each item is `ntyp` (number of types of atoms in the unit cell), `nat` (number of **all** atoms in the unit cell), `ibrav` (Bravais-lattice index), `celldm` (Crystallographic constants, from `celldm(1)` to `celldm(6)`), respectively.

Specially, if `ibrav` is `0`, then there will be 3 lines below to show the lattice constants, with each line containing 3 floating-point numbers.

The next 2 lines,

```
           1  'Al '    24590.765652728711     
           2  'As '    68285.402620549852  
```

are the type of atom, the atom’s name, and the atomic mass in Rydberg unit. The calculation method is like this: assume atomic mass in SI unit `AMU_SI` is `1.660538782E-27` kg, the electronic mass in SI unit `ELECTRONMASS_SI` is `9.10938215E-31` kg. Then the atomic mass in Hatree unit `AMU_AU` is `AMU_SI / ELECTRONMASS_SI`, while in Rydberg unit is half of the`AMU_AU`. So the number written in your `ph.x` input file is timed by `911.4442421322725` in the force constant output. Those constants are defined in `/path/to/qe-6.3/Modules/constants.f90`.

The next 2 lines, are the atomic positions in the cell:

```
    1    1      0.0000000000      0.0000000000      0.0000000000
    2    2      0.2500000000      0.2500000000      0.2500000000
```

The next line, could be either `T` (true) or `F` (false), indicating whether you have `zstar`. If `T`, First read the $3\times 3$ matrix `epsil` , then for each atom, read the effective charges. If `has_zstar` is `F`, no lines are given for this step.

The the line

```
   4   4   4
```

which are `nr1`, `nr2`, and `nr3`, respectively.

### Body

Now we come to the most important part: the force constant in the body.

Let’s come to the first line,

```
   1   1   1   1
```

this first 2 integers label the polarizations of the force constant matrix, and the last 2 integers label the number of atoms in the basis set.

After a number of lines we will have

```
   1   1   1   2
```

Between these 2 lines, are the force constant on each FFT grid-point (labeled by the first 3 indices), i.e., you will have $4\times 4\times 4 = 64$ lines between them.

The final force constant within one file will have shape `(nr1,nr2,nr3,3,3,nat,nat)`. In our $\ce{AlAs}$ case, this will be `(4,4,4,3,3,2,2)` .