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

# Kernel modules

## How to

#### List kernel modules

```
lsmod
```

```bash
cat /proc/modules
```

### Module info

{% hint style="warning" %}
This gives information of an installed module, it might be different from the inserted one
{% endhint %}

```
modinfo MODULE
```

Get info of an inserted module

```
ls -l /sys/module/<module>
```

### Check flags of kernel modules

[Kernel module flags](https://docs.kernel.org/admin-guide/tainted-kernels.html#more-detailed-explanation-for-tainting) are displayed with `cat /proc/modules`, flags are shown in parentheses

```
$ cat /proc/modules 
r8168 516096 0 - Live 0x0000000000000000 (OE)

```
