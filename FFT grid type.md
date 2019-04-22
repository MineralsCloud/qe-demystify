# FFT grid type

1. `grid_type = 'Dense'`: inverse fourier transform of potentials and charge density f on the dense grid. On output, f is overwritten
2. `grid_type = 'Smooth'`: inverse fourier transform of  potentials and charge density f on the smooth grid . On output, f is overwritten
3. `grid_type = 'Wave'`: inverse fourier transform of  wave functions f on the smooth grid . On output, f is overwritten  
4. `grid_type = 'tgWave'`: inverse fourier transform of  wave functions f with task group on the smooth grid . On output, f is overwritten
5. `grid_type = 'Custom'`: inverse fourier transform of potentials and charge density f on a custom grid. On output, f is overwritten
6. `grid_type = 'CustomWave'`: inverse fourier transform of  wave functions fon a custom grid. On output, f is overwritten

## References

1. [q-e/FFTXlib/fft_fwinv.f90](https://github.com/QEF/q-e/blob/master/FFTXlib/fft_fwinv.f90)
