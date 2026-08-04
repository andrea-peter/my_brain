# Build system

## Configuration

### Build a configuration

```
ARCH=arm64 make erx_tegra_defconfig
 ^                          ^
 |                          |
Specify architecture       Refers to arch/<ARCH>/config/erx_defconfig
```

this creates the repository `.config` that contains the _current config_

### Save minimal configuration

When modifying a configuration by hand in can be that it is not "normalized" or "not minimal"

```
ARCH=arm64 make savedefconfig
```

creates `defconfig` file which is the minimal/normalized config

## Clean

```
make clean     -  Cleans some things
make mrproper  -  Cleans everything except config
make distclean -  Cleans everthing
```

## Cross compilation

Example

```
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-
export PATH=<toolchain>/bin:$PATH
```

## Symbols

### Kernel

The symbols of the kernel itself (usually `mvlinux`) are contained in `System.map`  (created when kernel is built - `make`)

### Modules

Symbols exported by modules are in the file `Module.symvers` (created when modules are built - `make modules`) contains the exported symbols,&#x20;
