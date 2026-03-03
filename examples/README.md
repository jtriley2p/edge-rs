# Edge Examples

Each `.edge` file can be processed with `edgec`:

```sh
# Print the token stream
edgec lex <file.edge>

# Print the abstract syntax tree
edgec parse <file.edge>

# Compile to bytecode (once codegen is implemented)
edgec build <file.edge>
```

## Files

| File | Description |
|------|-------------|
| [`counter.edge`](./counter.edge) | Simple on-chain counter contract with increment/decrement/reset |
| [`erc20.edge`](./erc20.edge) | Minimal ERC-20 token skeleton with ABI declaration |
| [`types.edge`](./types.edge) | Showcase of all primitive types, data locations, type aliases, and constants |
| [`expressions.edge`](./expressions.edge) | Arithmetic, comparison, bitwise, and nested expression examples |

## Quick start

```sh
# Build the compiler
cargo build --bin edgec

# Run the counter example through the lexer
cargo run --bin edgec -- lex examples/counter.edge

# Run the types example through the parser
cargo run --bin edgec -- parse examples/types.edge
```
