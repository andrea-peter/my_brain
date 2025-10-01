# Rust

## Paths

```
~/.rustup
~/cargo
```

## Packages

[https://crates.io/](https://crates.io/)

## Rustup

Rust toolchain installer

### How to

Update run

```
rustup update
```

#### See documentation

```
rustup doc
```

#### Uninstall

```
rustup self uninstall
```

## Cargo

* Create new project: `cargo new <name>`
* Build project for development: `cargo build`
* Build project for release: `cargo build --release`
* Compile without producing output: `cargo build`
* Run your project: `cargo run`
* Test your project: `cargo test`
* Build documentation for your project: `cargo doc --open`
* Publish a library to [crates.io](https://crates.io): `cargo publish`

## Code organization

Package > Crate > Module

### Package

* Has _`Cargo.toml`_
* Bundle of one or more crates:
  * At most one library crate
  * Any number of binary crates

### Crate

Smallest compilable unit

* `src/main.rs`: root of binary crate with same name as the package
* `src/lib.rs`: root of library crate with same name as the package
* `src/bin/`: Binary crates
* `cargo new` creates a new package

### Module

* Start from the crate root (like the compiler does)
* Declare modules in the crate root, the compiler will look for:
  * Inline, with  `mod <mymodule> {...}`
  * `src/<mymodule>.rs`
  * `src/<mymodule>/mod.rs`
* One root module
* Code within a module is private from its parent module by default
*
