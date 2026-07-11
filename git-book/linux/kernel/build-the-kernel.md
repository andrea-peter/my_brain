---
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Build the kernel

## Prerequisites

### Toolchain

WARNING: The kernel sources are not forward compatible with the compiler, the minimal version is documented, example for Kernel 5.1: [https://docs.kernel.org/5.1/process/changes.html](https://docs.kernel.org/5.1/process/changes.html)

#### Local

Debain-based

```
sudo apt list install build-essential
```

Arch

```
sudo pacman -S base-devel
```

#### Cross-compile

TODO

## Download sources

Clone the repo [https://github.com/torvalds/linux](https://github.com/torvalds/linux)

## Config

### Toolchain config

GCC version

### Kernel config

#### Default config

```
make defconfig
```

#### Menu config

```
make menuconfig
```

## Clean

One pretty thorough clean is

```
make mrproper
```

