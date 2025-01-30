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

# Device Tree

OS-agnostic device representation for devices that are not discoverable (like devices on I2C, SPI etc.)

Sometimes the `of_` prefix appears, this is because the device tree was introduce by [OpenFirmware](https://en.wikipedia.org/wiki/Open_Firmware)

## Device tree source syntax

<div align="left"><figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure></div>

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## Inclusion

`.dtsi` files can be `#include`d into `.dts` files, the including file can override values specified by the included file

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

## Device tree compilation

The program `dtc` can compile a device tree from source to binary

<div align="left"><figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Device tree compilation</p></figcaption></figure></div>

```
dtc -I dts -O dtb -o foo.dtb foo.dts
```

### How to

### Compile a device tree source

```
dtc -I dts -O dtb -o foo.dtb foo.dts
```

### Explore the device tree on the target

The device tree is represented in a directory/file form in `/sys/firmware/devicetree/base`

### Get device tree source from filesystem

```
dtc -I fs /sys/firmware/devicetree/base
```

## Device tree on running system

DTBs are in `/boot/dtb`, not sure where they come from

## Links

[https://bootlin.com/pub/conferences/2021/webinar/petazzoni-device-tree-101/petazzoni-device-tree-101.pdf](https://bootlin.com/pub/conferences/2021/webinar/petazzoni-device-tree-101/petazzoni-device-tree-101.pdf)
