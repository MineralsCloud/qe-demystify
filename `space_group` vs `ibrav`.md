# `space_group` vs `ibrav`

There are two ways to specify the space group of a crystal in `&SYSTEM` namelist for `pw.x`
input, i.e., `space_group` and `ibrav`.

With `space_group` specified, `nat` should be the number of inequivalent atoms, that is, the
atoms in an asymmetric unit. The `ATOMIC_POSITIONS` card should have option `crystal_sg` and
also list inequivalent atoms. The outputs, generated atoms and symmetry operations, are
those in the primitive cell. So it may have fewer atoms and symmetry operations than what
ITA lists and what Vesta, etc., generates.

If you use `ibrav` and want to have the same result as the `space_group` one, list the atoms
in the primitive cell in `ATOMIC_POSITIONS` card with option `crystal`. This is because the
cells in
[`ibrav` are all primitive cells](https://www.quantum-espresso.org/Doc/INPUT_PW.html#idm199).
