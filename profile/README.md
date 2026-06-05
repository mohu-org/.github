<p align="center">
  <img src="../assets/mohu.png" alt="mohu" width="160">
</p>

# Mohu

Rust-powered arrays for Python. Fast, parallel, and built for the future.

Mohu is an early-stage rewrite of the Python numerical stack from the systems layer up. The core is written in Rust, with a focus on parallel execution, efficient memory layouts, first-class typed arrays, and clean Python integration.

## Why Mohu

Python's numerical ecosystem deserves a foundation that can take better advantage of modern hardware without making users leave the tools they already know.

Mohu is built around a few principles:

- Parallel operations by default
- Strong Rust internals with Python-facing ergonomics
- Zero-copy interop where possible
- SIMD-accelerated kernels
- First-class support for array types that are awkward in traditional NumPy-style layouts
- Clean boundaries between core arrays, compute kernels, linear algebra, and Python bindings

## Projects

| Repository | Purpose |
| --- | --- |
| [mohu](https://github.com/mohu-org/mohu) | Main array library and workspace for the Mohu ecosystem. |
| [mohu-compute](https://github.com/mohu-org/mohu-compute) | Standalone SIMD-accelerated compute kernels. |
| [mohu-linalg](https://github.com/mohu-org/mohu-linalg) | Pure-Rust linear algebra routines for Mohu and standalone use. |
| [mohu-py](https://github.com/mohu-org/mohu-py) | Python bindings with zero-copy NumPy interop via PyO3. |

## Direction

The goal is a practical NumPy-compatible array stack with a Rust-native core:

- N-dimensional arrays
- Parallel arithmetic and reductions
- Linear algebra
- Statistics and random routines
- Arrow-friendly memory and data interchange
- Python bindings that feel natural from day one

Mohu is still early. The foundation is being laid in public.

## Contributing

If you are interested in Rust, Python scientific computing, array internals, SIMD, Arrow, or numerical APIs, start with the [mohu](https://github.com/mohu-org/mohu) repository.

## License

Mohu projects are released under the MIT License.
