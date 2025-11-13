# 04 - U-Boot bootloader

## Get the right version of U-Boot

Pi-5 support was added to U-Boot v2024.04, however the LST YOCTO release Scarthgap by default provides U-Boot v2024.01.

Release Styhead from October 2024 provides U-Boot v2024.07.

Solution: add an extra layer that provides the right version of U-Boot: `meta-lts-mixins`

```
cd src/poky-rpi
git clone -b scarthgap/u-boot git://git.yoctoproject.org/meta-lts-mixins
```

## Proprietary bootloder

The Pi bootloader is proprietary, this bootloader loads U-Boot

## Configure to use U-Boot

Add the following line to `conf/local.conf`

```
RPI_USE_U_BOOT = "1"
```

## Re-build

This will take a long time

```
bitbake core-image-base
```
