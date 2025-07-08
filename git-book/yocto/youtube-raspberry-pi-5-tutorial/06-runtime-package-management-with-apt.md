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

# 06 - Runtime package management with apt

We can add runtime package management to our image

## Check current value of `PACKAGE_CLASSES`

```
$ bitbake-getvar PACKAGE_CLASSES
NOTE: Starting bitbake server...
#
# $PACKAGE_CLASSES [3 operations]
#   set? /home/andrea/git/poky-rpi/meta-poky/conf/distro/poky.conf:33
#     "package_rpm"
#   set? /home/andrea/git/poky-rpi/meta/conf/distro/defaultsetup.conf:16
#     "package_ipk"
#   set /home/andrea/git/poky-rpi/meta/conf/documentation.conf:315
#     [doc] "This variable specifies the package manager to use when packaging data. It is set in the conf/local.conf file in the Build Directory."
# pre-expansion value:
#   "package_rpm"
PACKAGE_CLASSES="package_rpm"
```

We want to use `deb` packages, add the following lines to `conf/local.conf`

```
PACKAGE_CLASSES = "package_deb"
EXTRA_IMAGE_FEATURES += "package-management"
```

Build, flash, reboot

## Build nano deb package

```
bitbake nano
```

Rebuild package index

```
bitbake package-index
```

The packages can be seen at `tmp/deploy/deb`

## Start http server on host PC to serve deb packages

```
cd tmp/deploy/deb
busybox httpd -p 8000 -f -vv
```

## Add PC as deb repository on the target

```
deb [trusted=yes] http://192.168.1.200:8000/all ./
deb [trusted=yes] http://192.168.1.200:8000/cortexa76 ./
deb [trusted=yes] http://192.168.1.200:8000/raspberrypi5 ./
```

Make sure IPs are set correctly

## Install nano on the target

```
# apt update
# apt install nano
```

{% hint style="info" %}
For some reason this does not work,

when doing `apt update`this happens on the target:

```
# apt install nano
Reading package lists... Done
Building dependency tree... Done
root@raspberrypi5:~# apt update
Ign:1 http://192.168.1.200:8000/all ./ InRelease
Ign:2 http://192.168.1.200:8000/cortexa76 ./ InRelease
Ign:3 http://192.168.1.200:8000/raspberrypi5 ./ InRelease
Get:4 http://192.168.1.200:8000/all ./ Release [1215 B]
Get:5 http://192.168.1.200:8000/cortexa76 ./ Release [1221 B]
Get:6 http://192.168.1.200:8000/raspberrypi5 ./ Release [1224 B]
Ign:7 http://192.168.1.200:8000/all ./ Release.gpg
Ign:8 http://192.168.1.200:8000/cortexa76 ./ Release.gpg
Ign:9 http://192.168.1.200:8000/raspberrypi5 ./ Release.gpg
Reading package lists... Done
E: Release file for http://192.168.1.200:8000/all/./Release is not valid yet (invalid for another 35d 17h 14min 37s). Updates for this repository will not be applied.
E: Release file for http://192.168.1.200:8000/cortexa76/./Release is not valid yet (invalid for another 35d 17h 14min 47s). Updates for this repository will not be applied.
E: Release file for http://192.168.1.200:8000/raspberrypi5/./Release is not valid yet (invalid for another 35d 17h 14min 38s). Updates for this repository will not be applied.
```

And this on the host (httpd output):

```
[::ffff:192.168.1.11]:44066: url:/all/InRelease
[::ffff:192.168.1.11]:44066: response:404
[::ffff:192.168.1.11]:44080: url:/cortexa76/InRelease
[::ffff:192.168.1.11]:44080: response:404
[::ffff:192.168.1.11]:44082: url:/raspberrypi5/InRelease
[::ffff:192.168.1.11]:44082: response:404
[::ffff:192.168.1.11]:44092: url:/all/Release
[::ffff:192.168.1.11]:44092: response:200
[::ffff:192.168.1.11]:44100: url:/cortexa76/Release
[::ffff:192.168.1.11]:44100: response:200
[::ffff:192.168.1.11]:44116: url:/raspberrypi5/Release
[::ffff:192.168.1.11]:44116: response:200
[::ffff:192.168.1.11]:44118: url:/all/Release.gpg
[::ffff:192.168.1.11]:44118: response:404
[::ffff:192.168.1.11]:44126: url:/cortexa76/Release.gpg
[::ffff:192.168.1.11]:44126: response:404
[::ffff:192.168.1.11]:44132: url:/raspberrypi5/Release.gpg
[::ffff:192.168.1.11]:44132: response:404
```
{% endhint %}
