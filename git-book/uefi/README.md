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
  tags:
    visible: true
---

# UEFI

[https://uefi.org/specs/UEFI/2.11/index.html](https://uefi.org/specs/UEFI/2.11/index.html)

## Boot manager

Loads applications or and drivers

### Applications

UEFI applications are loaded by the boot manager or other applications, they take control when loaded, when they terminate, the control goes back to the UEFI component that loaded the application

#### OS Loaders

UEFI OS loaders are a special king of applications that does not give back control

### Drivers

Loaded by the boot manager, firmware or applications.

Two types of drivers

* Boot service drivers
* Runtime drivers

Difference: Runtime drivers are available after the OS loader has taken control (the OS is booted)

## GUIDs

Each protocol has a unique GUID associated to it

## Handles

In the [data types specification](https://uefi.org/specs/UEFI/2.11/02_Overview.html#data-types) they are void pointers, a collection of related interfaces

Handles support protocols



## Protocols

[https://uefi.org/specs/UEFI/2.11/02\_Overview.html#protocols](https://uefi.org/specs/UEFI/2.11/02_Overview.html#protocols)

Composed of:

* GUID specific to the protocol
* Interface structure
* Protocol services

### PCD protocol

A platform database that contains a variety of current platform settings

***

## Links

### Krinkinmu's blog

* [https://krinkinmu.github.io/2020/10/11/efi-getting-started.html](https://krinkinmu.github.io/2020/10/11/efi-getting-started.html)
* [https://krinkinmu.github.io/2020/10/18/handles-guids-and-protocols.html](https://krinkinmu.github.io/2020/10/18/handles-guids-and-protocols.html)

### EDK II debugging

* [https://www.tianocore.org/tianocore-wiki.github.io/development/tutorials-howto/edk\_ii\_debugging.html](https://www.tianocore.org/tianocore-wiki.github.io/development/tutorials-howto/edk_ii_debugging.html)

### edk2 UEFI driver writers guide

* [https://github.com/tianocore-docs/edk2-UefiDriverWritersGuide/blob/main/SUMMARY.md](https://github.com/tianocore-docs/edk2-UefiDriverWritersGuide/blob/main/SUMMARY.md)

