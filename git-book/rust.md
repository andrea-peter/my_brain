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
* Must contain at least one crate:
  * At most one library crate
  * Any number of binary crates

### Crate

Smallest compilable unit

* `src/main.rs`: binary crate with same name as the package
* `src/lib.rs`: library crate with same name as the package
* `src/bin/`: All other binaries

### Module

* One root module
* Code within a module is private from its parent module by default
*
