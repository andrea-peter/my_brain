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

## dh\_dkms

This is a debhelper, Added in Ubuntu 24.04 (noble)

