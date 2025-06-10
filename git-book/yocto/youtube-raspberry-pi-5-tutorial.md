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

# YouTube Raspberry Pi 5 tutorial

[https://www.youtube.com/watch?v=fY7u6PiV8qA\&list=PLRsiDZNEIs\_T-AjQROqpwlzdLoJCkRab7](https://www.youtube.com/watch?v=fY7u6PiV8qA\&list=PLRsiDZNEIs_T-AjQROqpwlzdLoJCkRab7)

#### Clone YOCTO poky release

```
git clone -b scarthgap git://git.yoctoproject.org/poky poky-rpi
```

#### Clone BSP layer `meta-raspberrypi`

```
cd poky-rpi
git clone -b scarthgap https://github.com/agherzan/meta-raspberrypi.git
```

#### Setup environment

```
source oe-init-build-env
```

this should cd into `build/`

#### Add meta-raspberrypi layer

```
bitbake-layers add-layer ../meta-raspberrypi/
```

This should add the layer in `config/bblayers.conf`

#### Adjust `conf/local.conf`, append the following lines:

```
MACHINE = "raspberrypi5"

INIT_MANAGER = "systemd"

LICENSE_FLAGS_ACCEPTED = "synaptics-killswitch"
```

{% hint style="info" %}
On Ubuntu 24.04 you need to adjust an apparmor setting

Edit the file `/etc/sysctl.d/60_apparmor-namespace.conf`, add the following file:

```
kernel.apparmor_restrict_unprivileged_userns=0
```
{% endhint %}

#### Deactivate pyenv

First we need to deactivate pynev, otherwise we have the error:

```
pyenv/libexec/pyenv-exec: Argument list too long
```

so comment out the pyenv initialization in our `.bashrc`

#### Build image (this will take a lot of time the first time)

```
bitbake core-image-base
```

The images are output in

```
build/tmp/deploy/images/raspberyypi5/
```

