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

# dkms

dynamic kernel module support

## dkms.conf

Tells dkms how/where to build/install the module

## Paths

Sources are places at

```
/usr/src
```

Built dkms modules are placed at

```
/lib/modules/$(uname -r)/updates/dkms
```

## Workflow

```
dkms add
dkms build
dkms install
```

And the opposite:

```
dkms uninstall
dkms unbuild
dkms remove
```

### dkms add

Copies given sources to

```
/var/src/<module>-<module_version>/
```

### dkms build

Build takes place in

```
/var/lib/dkms/<module>/<version>/<kernel>/<arch>/
```

### dkms install

Install a built module into the kernel it was built for

## dh\_dkms

This is a debhelper, Added in Ubuntu 24.04 (noble)

