# `matdyn.x` input documentation

This documentation is read from the source code `q-e/PHonon/PH/matdyn.f90`.

This program calculates the phonon frequencies for a list of generic q vectors starting from the interatomic force constants generated from the dynamical matrices as written by DFPT phonon code through the companion program `q2r.x`.

`matdyn.x` can generate a supercell of the original cell for mass approximation calculation. If supercell data are not specified in input, the unit cell, lattice vectors, atom types and positions are read from the force constant file.

<table>
    <tbody>
        <tr>
            <th align="center">name</th>
            <th align="center">type</th>
            <th align="center">description</th>
        </tr>
        <tr>
            <td align="center"><code>flfrc</code></td>
            <td align="center">character</td>
            <td align="left">file produced by <code>q2r.x</code> containing force constants (needed). It is the same as in the input of <code>q2r.x</code> (+ the <code>.xml</code> extension if the dynamical matrices produced by <code>ph.x</code> were in xml format).<br>No default value: must be specified.</td>
        </tr>
        <tr>
            <td align="center"><code>asr</code></td>
            <td align="center">character</td>
            <td align="left">indicates the type of Acoustic Sum Rule imposed
                <ul>
                    <li><code>'no'</code>: no Acoustic Sum Rules imposed (default)</li>
                    <li><code>'simple'</code>: previous implementation of the asr used (3 translational asr imposed by correction of the diagonal elements of the force constants matrix)</li>
                    <li><code>'crystal'</code>: 3 translational asr imposed by optimized correction of the force constants (projection).</li>
                    <li><code>'one-dim'</code>: 3 translational asr + 1 rotational asr imposed by optimized correction of the force constants (the rotation axis is the direction of periodicity; it will work only if this axis considered is one of the cartesian axis).</li>
                    <li><code>'zero-dim'</code>: 3 translational asr + 3 rotational asr imposed by optimized correction of the force constants</li>
                </ul>
Note that in certain cases, not all the rotational asr can be applied (e.g. if there are only 2 atoms in a molecule or if all the atoms are aligned, etc.). In these cases the supplementary asr are cancelled during the orthonormalization procedure (see below).
            </td>
        </tr>
        <tr>
            <td align="center"><code>dos</code></td>
            <td align="center">logical</td>
            <td align="left">
                <ul>
                    <li>If <code>.true.</code> calculate phonon Density of States (DOS) using tetrahedra and a uniform q-point grid (see below).<br>NB: may not work properly in noncubic materials.</li> <li>If <code>.false.</code> calculate phonon bands from the list of q-points supplied in input (default)</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td align="center"><code>nk1,nk2,nk3</code></td>
            <td align="center">integer</td>
            <td align="left">uniform q-point grid for DOS calculation (includes q=0) (must be specified if <code>dos=.true.</code>, ignored otherwise)</td>
        </tr>
        <tr>
            <td align="center"><code>deltaE</code></td>
            <td align="center">real</td>
            <td align="left">energy step, in cm^(-1), for DOS calculation: from min to max phonon energy (default: 1 cm^(-1) if ndos, see below, is not specified)</td>
        </tr>
        <tr>
            <td align="center"><code>ndos</code></td>
            <td align="center">integer</td>
            <td align="left">number of energy steps for DOS calculations (default: calculated from <code>deltaE</code> if not specified)</td>
        </tr>
        <tr>
            <td align="center"><code>fldos</code></td>
            <td align="center">character</td>
            <td align="left">output file for dos (default: <code>'matdyn.dos'</code>)<br>the dos is in states/cm(-1) plotted vs omega in cm(-1) and is normalised to 3*nat, i.e. the number of phonons</td>
        </tr>
        <tr>
            <td align="center"><code>flfrq</code></td>
            <td align="center">character</td>
            <td align="left">output file for frequencies (default: <code>'matdyn.freq'</code>)</td>
        </tr>
        <tr>
            <td align="center"><code>flvec</code></td>
            <td align="center">character</td>
            <td align="left">output file for normalized phonon displacements (default: <code>'matdyn.modes'</code>). The normalized phonon displacements are the eigenvectors divided by the square root of the mass, then normalized. As such they are not orthogonal.</td>
        </tr>
        <tr>
            <td align="center"><code>fleig</code></td>
            <td align="center">character</td>
            <td align="left">output file for phonon eigenvectors (default: <code>'matdyn.eig'</code>)<br>The phonon eigenvectors are the eigenvectors of the dynamical matrix. They are orthogonal.
            </td>
        </tr>
        <tr>
            <td align="center"><code>fldyn</code></td>
            <td align="center">character</td>
            <td align="left">output file for dynamical matrix (default: <code>' '</code> i.e. not written)</td>
        </tr>
        <tr>
            <td align="center"><code>at</code></td>
            <td align="center">character</td>
            <td align="left">supercell lattice vectors - must form a superlattice of the original lattice (default: use original cell)</td>
        </tr>
        <tr>
            <td align="center"><code>l1,l2,l3</code></td>
            <td align="center">integer</td>
            <td align="left">supercell lattice vectors are original cell vectors times <code>l1</code>, <code>l2</code>, <code>l3</code> respectively (default: <code>1</code>, ignored if <code>at</code> specified)</td>
        </tr>
        <tr>
            <td align="center"><code>ntyp</code></td>
            <td align="center">integer</td>
            <td align="left">number of atom types in the supercell (default: <code>ntyp</code> of the original cell)
            </td>
        </tr>
        <tr>
            <td align="center"><code>amass</code></td>
            <td align="center">integer</td>
            <td align="left">masses of atoms in the supercell (a.m.u.), one per atom type (default: use masses read from file <code>flfrc</code>)</td>
        </tr>
        <tr>
            <td align="center"><code>readtau</code></td>
            <td align="center">logical</td>
            <td align="left">read atomic positions of the supercell from input (used to specify different masses) (default: <code>.false.</code>)</td>
        </tr>
        <tr>
            <td align="center"><code>fltau</code></td>
            <td align="center">logical</td>
            <td align="left">write atomic positions of the supercell to file <code>fltau</code> (default: <code>fltau=' '</code>, do not write)</td>
        </tr>
        <tr>
            <td align="center"><code>la2F</code></td>
            <td align="center">logical</td>
            <td align="left">if <code>.true.</code> interpolates also the el-ph coefficients.</td>
        </tr>
        <tr>
            <td align="center"><code>q_in_band_form</code></td>
            <td align="center">logical</td>
            <td align="left">if <code>.true.</code> the q points are given in band form: Only the first and last point of one or more lines are given. See below. (default: <code>.false.</code>).</td>
        </tr>
        <tr>
            <td align="center"><code>q_in_cryst_coord</code></td>
            <td align="center">logical</td>
            <td align="left">if <code>.true.</code> input q points are in crystalline coordinates (default: <code>.false.</code>)</td>
        </tr>
        <tr>
            <td align="center"><code>eigen_similarity</code></td>
            <td align="center">logical</td>
            <td align="left">use similarity of the displacements to order frequencies (default: <code>.false.</code>)<br>NB: You cannot use this option with the symmetry analysis of the modes.</td>
        </tr>
        <tr>
            <td align="center"><code>fd</code></td>
            <td align="center">logical</td>
            <td align="left">if <code>.t.</code> the ifc come from the finite displacement calculation</td>
        </tr>
        <tr>
            <td align="center"><code>na_ifc</code></td>
            <td align="center">logical</td>
            <td align="left">add non analitic contributions to the interatomic force constants if finite displacement method is used (as in Wang et al. Phys. Rev. B 85, 224303 (2012)) [to be used in conjunction with <code>fd.x</code>]</td>
        </tr>
    </tbody>
</table>

If `readtau` is `.true.`, atom types and positions in the supercell follow:

```fortran
(tau(i,na),i=1,3), ityp(na)
```

If `q_in_band_form` and `not dos` then

```fortran
nq     ! number of q points
(q(i,n),i=1,3), nptq   ! nptq is the number of points between this point and the next. These points are automatically generated. the q points are given in Cartesian coordinates, 2pi/a units (a=lattice parameters)
```

else, if only `not dos` is `.true.`, then

```fortran
nq      ! number of q-points
(q(i,n), i=1,3)   ! nq q-points in cartesian coordinates, 2pi/a units
                  !  If q = 0, the direction qhat (q=>0) for the non-analytic part is extracted from the sequence of q-points as follows: qhat = q(n) - q(n-1)  or   qhat = q(n) - q(n+1)
                  ! depending on which one is available and nonzero.
```

For low-symmetry crystals, specify twice `q = 0` in the list if you want to have `q = 0` results for two different directions.