# 07 - Create new layer and recipe

## Create layer

```
source oe-init-build-env
bitbake-layers create-layer ../meta-mylayer
bitbake-layers add-layer ../meta-mylayer
```

Convention for layers names is that they start with `meta-`&#x20;

## Create a recipe

```
cd ../meta-mylayer
mkdir -p recipes-apps/hello
vim recipes-apps/hello/hello_git.bb
```

With the following content:

```
DESCRIPTION = "Hello World"

# This is a hello world application written in C and built with autotools
HOMEPAGE = "https://github.com/leon-anavi/hello-world.git"
SECTION = "console/utils"
LICENSE = "MIT"
# Clone the repo and do "md5sum LICENSE"
LIC_FILES_CHKSUM = "file://LICENSE;md5=f388cad0df1af35e3626518d587c0cb6"
SRC_URI = "git://github.com/leon-anavi/hello-world.git;branch=master;protocol=https"
# SHA1 of the commit
SRCREV = "f66f58e7bcdcc834568d8c7c6fc51e30765befad"

S = "${WORKDIR}/git"

inherit autotools
```

Build

```
bitbake hello
```

## Extend existing recipe with our layer

Create file `meta-mylayer/recipes-core/images/core-image-base.bbappend` with the following content:

```
IMAGE_INSTALL:append = " hello"
```

Build

```
bitbake core-image-base
```
