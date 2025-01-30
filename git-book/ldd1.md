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

# LDD1

## Links

* Materials: [https://github.com/niekiran/linux-device-driver-1.git](https://github.com/niekiran/linux-device-driver-1.git)
* Slides: [https://1drv.ms/b/s!Akhv68fruLVPunnvLBoIL0-Gu-et?e=cCnfvr](https://1drv.ms/b/s!Akhv68fruLVPunnvLBoIL0-Gu-et?e=cCnfvr)
*

## Requirements

### Install deb packages

```
sudo apt update && sudo apt install build-essential lzop u-boot-tools net-tools bison flex gparted libssl-dev libncurses5-dev libncursesw5-dev unzip chrpath xz-utils minicom wget git-core
```

### Prepare directory structure

```
mkdir -p workspace/ldd/custom_drivers
mkdir -p workspace/ldd/downloads
mkdir -p workspace/ldd/patches
mkdir -p workspace/ldd/source
```

### Download

#### Boot image&#x20;

* [https://files.beagle.cc/file/beagleboard-public-2021/images/am335x-debian-11.7-iot-armhf-2023-09-02-4gb.img.xz](https://files.beagle.cc/file/beagleboard-public-2021/images/am335x-debian-11.7-iot-armhf-2023-09-02-4gb.img.xz)

#### Toolchain

* [https://snapshots.linaro.org/gnu-toolchain/14.0-2023.06-1/arm-linux-gnueabihf/gcc-linaro-14.0.0-2023.06-x86\_64\_arm-linux-gnueabihf.tar.xz.asc](https://snapshots.linaro.org/gnu-toolchain/14.0-2023.06-1/arm-linux-gnueabihf/gcc-linaro-14.0.0-2023.06-x86_64_arm-linux-gnueabihf.tar.xz.asc)

