<table>
  <tr>
    <td width="96">
      <img src="https://raw.githubusercontent.com/mohu-org/.github/main/assets/mohu.png" alt="Mohu" width="80">
    </td>
    <td>
      <h1>Mohu</h1>
    </td>
  </tr>
</table>

Rust-native array infrastructure for Python scientific computing.

Mohu is an early-stage attempt to rebuild the NumPy layer around modern systems primitives: typed buffers, explicit layouts, SIMD kernels, parallel execution, zero-copy exchange, and Python bindings that can interoperate with the existing data and ML ecosystem.

The project is being built as a set of small Rust crates instead of one monolith. Each layer owns a narrow part of the stack, from error types and dtype promotion through buffers, ufunc dispatch, indexing, linalg, sparse arrays, I/O, and Python protocols.

## Architecture

```text
Python surface
  mohu-py              PyO3 bindings, NumPy interop, buffer protocol, DLPack

Array API
  mohu-array           N-dimensional array type
  mohu-ufunc           broadcast, reduce, accumulate, outer
  mohu-index           fancy indexing, boolean masks, take/put, where
  mohu-ops             arithmetic, comparison, logical ops, reductions

Numerics
  mohu-linalg          matmul, LU, QR, SVD, Cholesky, solvers, eigensystems
  mohu-fft             FFT, IFFT, RFFT, N-D transforms
  mohu-random          PCG64, Philox, sampling, distributions
  mohu-stats           descriptive stats and statistical routines
  mohu-special         erf, gamma, beta, Bessel, CDF/PPF helpers

Storage and layout
  mohu-dtype           dtype model, scalar traits, promotion and casting
  mohu-buffer          aligned allocation, strides, views, DLPack metadata
  mohu-sparse          COO, CSR, CSC sparse matrices
  mohu-masked          masked arrays and invalid-value propagation
  mohu-io              .npy, CSV, Arrow IPC, memory-mapped arrays

Foundation
  mohu-error           shared error type, error codes, reporting, test helpers
  mohu-core            facade over the foundation crates
  mohu-testing         fixtures, approximate assertions, performance helpers
```

## Repositories

| Repository | Role |
| --- | --- |
| [mohu](https://github.com/mohu-org/mohu) | Main Rust workspace. Owns the layered crate architecture, roadmap, docs, tests, and core implementation. |
| [mohu-compute](https://github.com/mohu-org/mohu-compute) | Standalone SIMD compute kernels. Usable independently from Mohu array types. |
| [mohu-linalg](https://github.com/mohu-org/mohu-linalg) | Pure-Rust linear algebra backend with matmul, decompositions, norms, solvers, and eigen routines. |
| [mohu-py](https://github.com/mohu-org/mohu-py) | Python package surface and PyO3 bindings for zero-copy NumPy-facing workflows. |

## Interop Plan

Mohu is designed to meet existing Python libraries where they already are.

```text
mohu-buffer exposes pointer, shape, strides, dtype, device
  -> Python buffer protocol and __array__
  -> __array_interface__
  -> __dlpack__ and __dlpack_device__
  -> Array API Standard via __array_namespace__
  -> NumPy dispatch through __array_ufunc__ and __array_function__
```

That path is meant to unlock zero-copy handoff into NumPy, Pandas, scikit-learn, PyTorch, JAX, CuPy, TensorFlow, and other tools without forcing each library to know about Mohu directly.

## Current Focus

Mohu is pre-release. The active work is the foundation:

- dtype and scalar promotion rules
- aligned buffers, layouts, strides, and views
- DLPack-compatible metadata
- core array shape and slicing behavior
- broadcast and reduction machinery
- SIMD and parallel kernel paths
- Python bindings and NumPy interop

The goal is not a thin wrapper around existing arrays. The goal is a Rust-native array engine with Python ergonomics and standard protocol compatibility.

## Start Here

- Read the main workspace: [mohu](https://github.com/mohu-org/mohu)
- Review the crate ownership map: [CRATE_MAP.md](https://github.com/mohu-org/mohu/blob/main/CRATE_MAP.md)
- Check the roadmap: [ROADMAP.md](https://github.com/mohu-org/mohu/blob/main/ROADMAP.md)
- Contribute through the main repo: [CONTRIBUTING.md](https://github.com/mohu-org/mohu/blob/main/CONTRIBUTING.md)

## Build Principles

- Rust owns memory, layout, dtype, dispatch, and kernels.
- Python gets a familiar array API, not a second-class wrapper.
- Interop should be protocol-based and zero-copy where possible.
- Standalone crates should remain useful outside the full Mohu stack.
- Performance work should be measured with benchmarks, not asserted.

## License

Mohu projects are released under the MIT License.
