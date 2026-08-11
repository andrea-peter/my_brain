# Beaglebone Black

## Download prerequisites

### Official images

[https://www.beagleboard.org/distros](https://www.beagleboard.org/distros)

### bb-imager

[https://github.com/beagleboard/bb-imager/tree/main](https://github.com/beagleboard/bb-imager/tree/main)

### Toolchain

[https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/15.3.rel1/arm-gnu-toolchain-15.3.rel1-x86\_64-arm-none-linux-gnueabihf.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/15.3.rel1/arm-gnu-toolchain-15.3.rel1-x86_64-arm-none-linux-gnueabihf.tar.xz)

## Build kernel

### Install dependencies

* `mkimage`

### Configure env

{% code overflow="wrap" %}
```bash
export ARCH=arm
export CROSS_COMPILE=arm-none-linux-gnueabihf-
export PATH=<path-to-toolchain>/bin/:$PATH
```
{% endcode %}

### Check out source code

{% code overflow="wrap" %}
```bash
git clone https://github.com/beagleboard/linux.git
git checkout 6.6.58-ti-rt-arm32-r15  # rt means real-time(RT_PREEMPT)
```
{% endcode %}

### Configure

{% code overflow="wrap" %}
```bash
make bb.org_defconfig
make menuconfig
```
{% endcode %}

### Build

{% code overflow="wrap" %}
```bash
make -j12 LOADADDR=0x80000000 uImage dtbs
make -j12 modules
make modules_install
```
{% endcode %}

## How to

### Flash image to SD card

List available SD cards

```
$ bb-imager-cli list-destinations sd
+-------------------------+----------+-------------+
| SD Card                 | Path     | Size (in G) |
+-------------------------+----------+-------------+
| Generic-Multiple Reader | /dev/sda |          57 |
+-------------------------+----------+-------------+
```

Flash

{% code overflow="wrap" %}
```
$ sudo bb-imager-cli flash sd --timezone +1 --user-name user --user-password password ~/Downloads/am335x-debian-13.6-base-v6.18-armhf-2026-07-24-4gb.img.xz /dev/sda
[1] Preparing  
[2] Flashing                           100%
```
{% endcode %}

## Resources

[https://embetronicx.com/tutorials/linux/device-drivers/setup-beaglebone-board-linux-device-driver-tutorial/](https://embetronicx.com/tutorials/linux/device-drivers/setup-beaglebone-board-linux-device-driver-tutorial/)

[https://embeddedinventor.com/a-complete-beginners-guide-to-the-gnu-arm-toolchain-part-1/](https://embeddedinventor.com/a-complete-beginners-guide-to-the-gnu-arm-toolchain-part-1/)

