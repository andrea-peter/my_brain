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

# Kernel

## How to

### See console log level

```
$ cat /proc/sys/kernel/printk
4        4        1        7

# current default minimum boot-time-default log levels.
```



### Get information about running kernel

#### Get kernel version

```
uame -r
```

#### Get configuration of running kernel

Can be found in one of

```
/proc/config.gz
/boot/config
/boot/config-$(uname -r)
```

It might be necessary to load a kernel module first:

```
modprobe configs
```

#### Get current device tree

```
dtc -I fs /sys/firmware/devicetree/base/
```

## Includes

### UAPI

User space API of the kernel
