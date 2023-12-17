# Avoid oversubscribing threads

If you find that the number of processor cores reported by QE is much larger than the
number of physical cores your machine has, and you are experiencing very sluggish
output, this could indicate thread oversubscription.

Thread oversubscription occurs when the operating system frequently switches between
threads (context switching) to create the illusion of simultaneous execution.
This can lead to performance issues due to the overhead of context switching and the
CPU's inability to handle all threads effectively.

It is likely that the OpenMP parallelization is interfering with
MPI. Recent versions of MKL, by default, enable autoparallelization on multicore machines.

If necessary, set the following environment variables:

```shell
export OMP_NUM_THREADS=1
export MKL_NUM_THREADS=1
export OPENBLAS_NUM_THREADS=1
```

## References

1. [Trouble with MKL and MPI parallelization](https://www.quantum-espresso.org/Doc/user_guide/node22.html#SECTION00045020000000000000)
2. [How to "Fill the CPU with OpenMP threads" to run QE-GPU?](https://mattermodeling.stackexchange.com/questions/6859/how-to-fill-the-cpu-with-openmp-threads-to-run-qe-gpu)
3. [Avoid Oversubscribing Threads](https://docs.dask.org/en/stable/array-best-practices.html#avoid-oversubscribing-threads)
