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

# Yocto

{% hint style="info" %}
To sort out
{% endhint %}

## Intro and terminology

### Yocto

Community project that works on BitBake, OpenEmbedded core, BSPs, tooling, etc.

### OpenEmbedded

Predates Yocto, _OpenEmbedded Core_ is a collection of essential recipes to build systems

### BitBake

Task executor and scheduler



## Append file

Append build info to a recipe file

* `.bbappend`
* There must be a corresponding `.bb` file

## How to

### Create build directory

[https://docs.yoctoproject.org/ref-manual/terms.html#term-Build-Directory](https://docs.yoctoproject.org/ref-manual/terms.html#term-Build-Directory)

### Create dependency graph

[https://docs.yoctoproject.org/bitbake/2.12/bitbake-user-manual/bitbake-user-manual-intro.html#generating-dependency-graphs](https://docs.yoctoproject.org/bitbake/2.12/bitbake-user-manual/bitbake-user-manual-intro.html#generating-dependency-graphs)

Build with `-g` option

```
bitbake -g core-image-base
```

Convert `.dot` to graphical file with `graphviz`

```
dot -Tps task-depends.dot task-depends.ps
```

## Layer

* A collection of recipes
* Can contain other layers (container layer)

{% hint style="info" %}
Some container layers are actual layers, other are just a folder
{% endhint %}

### Structure

```
.
├── conf
│   └── layer.conf
├── COPYING.MIT
├── README
└── recipes-example
    └── example
        └── example_0.1.bb
```

* `conf/layer.conf` : Main config file&#x20;
* `COPYING.MIT` : License file
* `README`:  Readme file
* `recipes_example/example/example_01.bb`: Recipe example

## Recipe

{% hint style="danger" %}
Isn't there any namespace by layer?
{% endhint %}

## [Images](https://docs.yoctoproject.org/4.0.27/ref-manual/images.html#images)

When the `bitbake` command is issued a "top-level" recipe is provided that essentially begins the build for the wanted image type.

Image recipes can be found with:

```
ls meta*/recipes*/images/*.bb
```

## Links

Layer index: [https://layers.openembedded.org/](https://layers.openembedded.org/)

All in one megamanual: [https://docs.yoctoproject.org/singleindex.html](https://docs.yoctoproject.org/singleindex.html)

### YOCTO

[https://docs.yoctoproject.org/](https://docs.yoctoproject.org/)

Scale 15 presentation slides:

* [Intro to the YOCTO project](https://docs.google.com/presentation/d/1LmI3mHoD_Dzl8wplIYcUBrFF8BzDb_EadTvfbnpSK7Q/edit?pli=1\&slide=id.p4#slide=id.p4)
* [YOCTO project advanced course](https://docs.google.com/presentation/d/1HoDtyN5SzlmuTN47ab4Y7w_i6c_VEW6EBUD944ntf38/edit?slide=id.p4#slide=id.p4)

### BitBake

Doc: [https://docs.yoctoproject.org/bitbake.html](https://docs.yoctoproject.org/bitbake.html)

Bitbake variables:\
[https://the-pi-guy.com/blog/bitbake\_variables\_and\_their\_impact\_on\_build\_processes/](https://the-pi-guy.com/blog/bitbake_variables_and_their_impact_on_build_processes/)







