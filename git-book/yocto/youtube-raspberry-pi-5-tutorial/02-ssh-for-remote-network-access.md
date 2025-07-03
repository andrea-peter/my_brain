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

# 02 - SSH for remote network access

[https://www.youtube.com/watch?v=ltckiBV9FXg\&list=PLRsiDZNEIs\_T-AjQROqpwlzdLoJCkRab7\&index=2\&pp=iAQB](https://www.youtube.com/watch?v=ltckiBV9FXg\&list=PLRsiDZNEIs_T-AjQROqpwlzdLoJCkRab7\&index=2\&pp=iAQB)

## Initialize env

```
cd git/poky-rpi/
source oe-init-build-env
```

## Get [bitbake variable](https://the-pi-guy.com/blog/bitbake_variables_and_their_impact_on_build_processes/) `EXTRA_IMAGE_FEATURES`

```
$ bitbake-getvar EXTRA_IMAGE_FEATURES
NOTE: Starting bitbake server...
#
# $EXTRA_IMAGE_FEATURES [3 operations]
#   set? /home/andrea/git/poky-rpi/build/conf/local.conf:149
#     "debug-tweaks"
#   set /home/andrea/git/poky-rpi/meta/conf/documentation.conf:163
#     [doc] "The list of additional features to include in an image. Configure this variable in the conf/local.conf file in the Build Directory."
#   set /home/andrea/git/poky-rpi/meta/conf/bitbake.conf:912
#     [_defaultval] ""
# pre-expansion value:
#   "debug-tweaks"
EXTRA_IMAGE_FEATURES="debug-tweaks"
```

Contains only value `debug-tweaks`

## Append to `EXTRA_IMAGE_FEATURES` variable

Modify `build/conf/local.conf`, add this line:

{% hint style="danger" %}
Don't forget to prepend a space in the value when using `:append`
{% endhint %}

```
EXTRA_IMAGE_FEATURES:append = " ssd-dropbear"
```

Now we can see the new value:

{% hint style="info" %}
We also see where the variable has been modified
{% endhint %}

```
$ bitbake-getvar EXTRA_IMAGE_FEATURES
NOTE: Starting bitbake server...
#
# $EXTRA_IMAGE_FEATURES [4 operations]
#   set? /home/andrea/git/poky-rpi/build/conf/local.conf:149
#     "debug-tweaks"
#   :append /home/andrea/git/poky-rpi/build/conf/local.conf:296
#     " ssh-server-dropbear"
#   set /home/andrea/git/poky-rpi/meta/conf/documentation.conf:163
#     [doc] "The list of additional features to include in an image. Configure this variable in the conf/local.conf file in the Build Directory."
#   set /home/andrea/git/poky-rpi/meta/conf/bitbake.conf:912
#     [_defaultval] ""
# pre-expansion value:
#   "debug-tweaks ssh-server-dropbear"
EXTRA_IMAGE_FEATURES="debug-tweaks ssh-server-dropbear"
```

## Re-build

```
bitbake core-image-base
```

This time the build takes a lot less time

## Re-flash

See lesson 01

It is now possible to connect via SSH (if IP addresses are set-up correctly)

