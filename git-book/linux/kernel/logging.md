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

# Logging

[https://www.kernel.org/doc/html/latest/core-api/printk-basics.html](https://www.kernel.org/doc/html/latest/core-api/printk-basics.html)

[https://unix.stackexchange.com/questions/214348/significance-of-linux-kernels-default-console-loglevel](https://unix.stackexchange.com/questions/214348/significance-of-linux-kernels-default-console-loglevel)

[https://elinux.org/Debugging\_by\_printing](https://elinux.org/Debugging_by_printing)



## Dynamic debug

[https://www.kernel.org/doc/html/latest/admin-guide/dynamic-debug-howto.html](https://www.kernel.org/doc/html/latest/admin-guide/dynamic-debug-howto.html)

[https://documentation.suse.com/sles/15-SP4/html/SLES-all/cha-tuning-dynamic-debug.html](https://documentation.suse.com/sles/15-SP4/html/SLES-all/cha-tuning-dynamic-debug.html)

Check if enabled

```
zcat /proc/config.gz | grep CONFIG_DYNAMIC_DEBUG
```

## Console log level

```
# cat /proc/sys/kernel/printk
6	6	1	7
```

current, default, minimum, boot-time-default log-levels

To set, write an integer to the file:

```
# cat 8 >/proc/sys/kernel/pritnk
```

or&#x20;

```
dmesg -n 8
```

{% hint style="info" %}
Not usre about these

```
dmesg --console-on
dmesg --console-off
```
{% endhint %}

### dmesg

```
dmesg -n LOG_LEVEL
```
