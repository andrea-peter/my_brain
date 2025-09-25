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
  metadata:
    visible: true
---

# apt - package manager

```
man apt
man apt_preferences
```

[https://wiki.debian.org/AptConfiguration](https://wiki.debian.org/AptConfiguration)

## Default release

Stored in the config: `APT::Default-Release`

## Package priority

```
man apt_preferences
```

* Used to decide which **package version** to install
* Bigger number: bigger priority
* Default is 500
* Default release packages have 990
* If packages have different priorities: the one with the highest priority is installed
* If packages have same priority: the one with the highest version is installed
* Pinning allows to change package priority for some packages/repositories

## How to

### See package priority

```
apt-cache policy PACKAGE
```
