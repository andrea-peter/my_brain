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

# 03 - Docker on Raspberry Pi 5

[https://www.youtube.com/watch?v=kQnOidK\_U3M\&list=PLRsiDZNEIs\_T-AjQROqpwlzdLoJCkRab7\&index=3](https://www.youtube.com/watch?v=kQnOidK_U3M\&list=PLRsiDZNEIs_T-AjQROqpwlzdLoJCkRab7\&index=3)

## Download source code of needed layers

The [meta-virtualization](https://layers.openembedded.org/layerindex/branch/master/layer/meta-virtualization/) layer depends on [meta-openembedded](https://layers.openembedded.org/layerindex/branch/master/layer/openembedded-core/), so we need to clone both their [web](https://layers.openembedded.org/layerindex/branch/master/layer/openembedded-core/) [repos](https://layers.openembedded.org/layerindex/branch/master/layer/meta-virtualization/)

```
cd git/poky-rpi
git clone -b scarthgap git://git.openembedded.org/meta-openembedded
git clone -b scarthgap git://git.yoctoproject.org/meta-virtualization
```

{% hint style="warning" %}
Question: on the meta-virtualization website there are other dependencies, are they already satisfied? How do we check that?
{% endhint %}

## Add needed layers

Currently we have the following layers:

```
$ bitbake-layers show-layers
NOTE: Starting bitbake server...
layer                 path                                                                    priority
========================================================================================================
core                  /home/andrea/git/poky-rpi/meta                                          5
yocto                 /home/andrea/git/poky-rpi/meta-poky                                     5
yoctobsp              /home/andrea/git/poky-rpi/meta-yocto-bsp                                5
raspberrypi           /home/andrea/git/poky-rpi/meta-raspberrypi                              9
```

We need to add more, when a layer is added, the dependencies are checked, here for example is does not work

```
$ bitbake-layers add-layer ../meta-openembedded/meta-python/
NOTE: Starting bitbake server...
ERROR: Layer 'meta-python' depends on layer 'openembedded-layer', but this layer is not enabled in your configuration
ERROR: Parse failure with the specified layer added, exiting.
```

We must add the layers in the right orders

```
$ bitbake-layers add-layer ../meta-openembedded/meta-oe/
NOTE: Starting bitbake server...
$ bitbake-layers add-layer ../meta-openembedded/meta-python/
NOTE: Starting bitbake server...
$ bitbake-layers add-layer ../meta-openembedded/meta-networking/
NOTE: Starting bitbake server...
$ bitbake-layers add-layer ../meta-openembedded/meta-filesystems/
NOTE: Starting bitbake server...
$ bitbake-layers add-layer ../meta-virtualization/
NOTE: Starting bitbake server...
```

## Modify variables in local config

```
DISTRO_FEATURES:append = " virtualization"

IMAGE_INSTALL:append = " docker-moby"
```

## Re-build

```
bitbake core-image-bake
```

## Resize root partition to take up remaining space

With gparted

## Docker demo

You board must have internet access

```
docker run -it hello-world
```



