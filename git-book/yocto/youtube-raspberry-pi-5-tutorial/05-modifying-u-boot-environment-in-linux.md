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
---

# 05 - Modifying U-Boot environment in Linux

We need `fw_printenv` and `fw_setenv`, for this we have to modify config, add this line to `conf/local.conf`

```
IMAGE_INSTALL:append = " u-boot-fw-utils u-boot-env"
```

Then build, flash and reboot.

It is now possible to modify U-Boot's environment in Linux
