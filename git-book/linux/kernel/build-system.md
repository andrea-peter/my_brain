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
