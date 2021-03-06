# ROPTLIB
ROPTLIB: Riemannian Manifold Optimization Library


The library is used to solve an optimization problem

f(x), x \in \mathcal{M},

where \mathcal{M} is a Riemannian manifold.

The detalied instruction and user manual can be found at http://www.math.fsu.edu/~whuang2/Indices/index_ROPTLIB.html.

## Fork changelog
- [cwrapper/blas/f2c.h](https://github.com/bbrrck/ROPTLIB/blob/master/cwrapper/blas/f2c.h) (for integration with Eigen)
  - change `typedef real` to `typedef rreal`
  - `#undef abs` at the end (otherwise conflict with `<complex>`)
- [CMakeLists.txt](https://github.com/bbrrck/ROPTLIB/blob/master/CMakeLists.txt)
