**Build status**: [![][gitlab-img]][gitlab-url]

[gitlab-img]: https://gitlab.com/JuliaGPU/CuYao.jl/badges/master/pipeline.svg
[gitlab-url]: https://gitlab.com/JuliaGPU/CuYao.jl/pipelines

CUDA support for [Yao.jl](https://github.com/QuantumBFS/Yao.jl).

**We are in an early-release beta. Expect some adventures and rough edges.**

## Installation

<p>
CuYao is a &nbsp;
    <a href="https://julialang.org">
        <img src="https://julialang.org/favicon.ico" width="16em">
        Julia Language
    </a>
    &nbsp; package. It provides CUDA support for <a href="https://github.com/QuantumBFS/Yao.jl">Yao.jl</a>. To install CuYao,
    please <a href="https://docs.julialang.org/en/v1/manual/getting-started/">open
    Julia's interactive session (known as REPL)</a> and press <kbd>]</kbd> key in the REPL to use the package mode, then type the following command
</p>

For stable release

```julia
pkg> add CuYao
```

For current master

```julia
pkg> add CuYao#master
```

You don't need to install Yao if you have `CuYao` installed. They share the same API except CUDA backend.

## Documentation

For documentation of [Yao](https://github.com/QuantumBFS/Yao.jl), please refer to [documentation (stable)](https://quantumbfs.github.io/Yao.jl/stable).

`CuYao.jl` provides only two extra APIs, `reg |> cu` to upload a register to GPU, and `cureg |> cpu` to download a register to CPU.

To start, see the following example
```julia
using CuYao

cureg = rand_state(9; nbatch=1000) |> cu 
cureg |> put(9, 2=>Z)
measure!(cureg |> addbits!(1) |> focus!(4,1,3))
cureg |> relax!(4,1,3) |> cpu
```

## Features
### Supported Gates

- general U(N) gate
- general U(1) gate
- better X, Y, Z gate
- better T, S gate
- SWAP gate
- better control gates
- BP diff blocks

### Supported Register Operations
- measure!, measure_reset!, measure_remove!, select
- addbit!
- insert_qubit!
- focus!, relax!
- join
- density_matrix

### Other Operations
- statistic functional diff blocks
- expect for statistic functional

## The Team

This project is an effort of QuantumBFS, an open source organization for quantum science. Yao is currently maintained by [Xiu-Zhe (Roger) Luo](https://github.com/Roger-luo) and [Jin-Guo Liu](https://github.com/GiggleLiu) with contributions from open source community. All the contributors are listed in the [contributors](https://github.com/QuantumBFS/Yao.jl/graphs/contributors).

## License

**CuYao** is released under the Apache 2 license.
