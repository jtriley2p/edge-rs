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

## Introductory examples

These top-level files cover the basics of Edge syntax and are the right place to start.

| File | Description |
|------|-------------|
| [`counter.edge`](./counter.edge) | Simple on-chain counter contract with increment/decrement/reset |
| [`types.edge`](./types.edge) | All primitive types, data location annotations, type aliases, and constants |
| [`expressions.edge`](./expressions.edge) | Arithmetic, comparison, bitwise, and nested expression examples |

## Modular examples — `lib/` and `tokens/`

The `lib/` and `tokens/` subdirectories contain a set of composable contracts inspired by [solmate](https://github.com/transmissions11/solmate). They use the full breadth of Edge's modularity features: `mod`, `use`, `abi`, `trait`, `event`, `indexed`, `contract`, and explicit `&s` storage annotations.

### `lib/` — foundational primitives

| File | Description |
|------|-------------|
| [`lib/math.edge`](./lib/math.edge) | WAD (1e18) and RAY (1e27) fixed-point math, `mul_div_down`/`mul_div_up`, safe add/sub, `min`/`max`/`clamp` |
| [`lib/auth.edge`](./lib/auth.edge) | `IOwned` and `IAuth` traits; `Owned` (two-step transfer) and `Auth` (owner + external authority) contracts |
| [`lib/safe_transfer.edge`](./lib/safe_transfer.edge) | `SafeERC20` trait and helpers for safe ERC-20 and ETH transfers |

### `tokens/` — ERC standard implementations

| File | Description | Imports |
|------|-------------|---------|
| [`tokens/erc20.edge`](./tokens/erc20.edge) | Full ERC-20 with events, `IERC20` abi, `ERC20Hooks` trait, internal `_mint`/`_burn`/`_transfer` | `lib::math`, `lib::auth` |
| [`tokens/erc721.edge`](./tokens/erc721.edge) | Full ERC-721 with three-event system, `IERC721Receiver` abi, `ERC721Base` trait | `lib::auth` |
| [`tokens/erc4626.edge`](./tokens/erc4626.edge) | ERC-4626 tokenized vault with `VaultMath` trait, `convertToShares`/`convertToAssets`, deposit/withdraw/redeem | `lib::math`, `lib::safe_transfer`, `lib::auth`, `tokens::erc20` |

### Import graph

```
tokens/erc4626 ──► lib/math
                ──► lib/safe_transfer ──► tokens/erc20 (IERC20)
                ──► lib/auth          (IOwned)
                ──► tokens/erc20      (IERC20)

tokens/erc20   ──► lib/math
               ──► lib/auth           (IOwned)

tokens/erc721  ──► lib/auth           (IOwned)
```

## Quick start

```sh
# Build the compiler
cargo build --bin edgec

# Introductory examples
cargo run --bin edgec -- lex examples/counter.edge
cargo run --bin edgec -- parse examples/types.edge

# Library modules
cargo run --bin edgec -- lex examples/lib/math.edge
cargo run --bin edgec -- parse examples/lib/auth.edge

# Token contracts
cargo run --bin edgec -- parse examples/tokens/erc20.edge
cargo run --bin edgec -- parse examples/tokens/erc721.edge
cargo run --bin edgec -- parse examples/tokens/erc4626.edge
```
