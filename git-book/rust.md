---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

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
