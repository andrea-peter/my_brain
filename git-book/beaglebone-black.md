# Beaglebone Black

## Download prerequisites

### Official images

[https://www.beagleboard.org/distros](https://www.beagleboard.org/distros)

### bb-imager

[https://github.com/beagleboard/bb-imager/tree/main](https://github.com/beagleboard/bb-imager/tree/main)

### Toolchain

TODO: something from here [https://gitlab.arm.com/tooling/gnu-toolchains-for-arm](https://gitlab.arm.com/tooling/gnu-toolchains-for-arm)

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

