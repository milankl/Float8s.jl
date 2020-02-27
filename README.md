[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://img.shields.io/badge/repo_status-active-brightgreen?style=flat-square)](https://www.repostatus.org/#active)
[![Travis](https://img.shields.io/travis/com/milankl/Float8s.jl?label=Linux%20%26%20osx&logo=travis&style=flat-square)](https://travis-ci.com/milankl/Float8s.jl)
[![AppVeyor](https://img.shields.io/appveyor/ci/milankl/Float8s-jl?label=Windows&logo=appveyor&logoColor=white&style=flat-square)](https://ci.appveyor.com/project/milankl/Float8s-jl)
[![Cirrus CI](https://img.shields.io/cirrus/github/milankl/Float8s.jl?label=FreeBSD&logo=cirrus-ci&logoColor=white&style=flat-square)](https://cirrus-ci.com/github/milankl/Float8s.jl)

# Float8s.jl
Finally a number type that you can count with your fingers. Super Mario and Zelda would be proud.

Comes in two flavours: `Float8` has 3 exponent bits and 4 fraction bits, `Float8_4` has 4 exponent bits and 3 fraction bits.
Both rely on conversion to Float32 to perform any arithmetic operation, similar to `Float16`.

# Example use

```julia
julia> using Float8s

julia> a = Float8(4)
Float8(4.0)

julia> b = Float8(3.14159)
Float8(3.125)

julia> a+b
Float8(7.0)

julia> sqrt(a)
Float8(2.0)

julia> a^2
Inf8
```
Most arithmetic operations are implemented. If you would like to have an additional feature, raise an [issue](https://github.com/milankl/Float8s.jl/issues).

# Installation

`Float8s.jl` is registered, just do
```julia
(v1.3) pkg> add Float8s
```

# Benchmarking
```julia
julia> using BenchmarkTools

julia> A = Float8.(randn(300,300));

julia> @btime Float32.($A);
  413.303 μs (2 allocations: 351.64 KiB)

julia> 413.303/300^2*1000
4.592255555555555
```
Conversions from Float8 to Float32 take about 4.5ns, conversions in the other direction are about 2x slower and slightly slower than for `Float16`. 
```julia
julia> A = Float32.(randn(300,300));

julia> @btime Float16.($A);
  674.123 μs (2 allocations: 175.89 KiB)

julia> @btime Float8.($A);
  955.196 μs (2 allocations: 88.02 KiB)
 ```
 
