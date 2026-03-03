# edge-rs

[![CI]][actions]
[![License]][mit-license]

[CI]: https://img.shields.io/github/actions/workflow/status/refcell/edge-rs/ci.yml?branch=main&label=ci
[actions]: https://github.com/refcell/edge-rs/actions?query=branch%3Amain
[License]: https://img.shields.io/badge/license-MIT-7795AF.svg
[mit-license]: https://github.com/refcell/edge-rs/blob/main/LICENSE.md

**edge-rs** is a compiler for the [Edge language](https://edgelang.netlify.app/) — an EVM-targeted DSL for writing smart contracts with a Rust-like type system.

**[Install](#install)**
| [Examples](#examples)
| [Contributing](#contributing)
| [License](#license)

## What is Edge?

Edge is a statically-typed, Rust-inspired language that compiles to EVM bytecode. It features:

- **EVM-native types** — `u8`–`u256`, `i8`–`i256`, `b1`–`b32`, `addr`, `bool`, `bit`
- **Data locations** — `&s` (storage), `&t` (transient), `&m` (memory), `&cd` (calldata)
- **Contracts & ABIs** — first-class `contract` and `abi` declarations
- **Traits & generics** — `trait`, `impl`, and type parameters
- **Pattern matching** — `match` with union types
- **Comptime** — compile-time evaluation via `comptime`

## Install

Install the Edge toolchain via `edgeup`:

```sh
curl -fsSL https://raw.githubusercontent.com/refcell/edge-rs/main/etc/install.sh | sh
```

Or build from source:

```sh
cargo install --path bin/edgec
```

## Examples

See the [`examples/`](./examples/) directory for complete Edge programs.

```sh
# Lex a file (print tokens)
edgec lex examples/counter.edge

# Parse a file (print AST)
edgec parse examples/counter.edge

# Compile a file
edgec build examples/counter.edge
```

## Contributing

All contributions are welcome. Open an issue or pull request on [GitHub](https://github.com/refcell/edge-rs).

## License

This project is licensed under the [MIT License](LICENSE.md).
