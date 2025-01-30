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

# Dynamic debug

## Mechanic

### Compilation

The `pr_debug` macro is conditionally compiled

* If `DYNAMIC_DEBUG[_MODULE]` is defined: it is compiled into the dynamic debug system
* Else-if `DEBUG` is defined: it is compiled as `printk(KERN_DEBUG`
* Else: Compiled out (deactivated)

### Activation

See: [https://www.kernel.org/doc/html/latest/admin-guide/dynamic-debug-howto.html](https://www.kernel.org/doc/html/latest/admin-guide/dynamic-debug-howto.html)

```
cat <debug_fs>/dynamic_debug_control
```

Prints all available `pr_debug` macros in the code that has been compiled with dynamic debug support and its flags

```
echo 'module <mymodule> > /sys/kernel/debug/dynamic_debug/control'
```

## Compilation options

* `DYNAMIC_DEBUG_CORE`: Enable core functionality but don't do anything
* `DYNAMIC_DEBUG:` Enable system-wide
* `DYNAMIC_DEBUG_MODULE`: Enable for module

### System-wide

Enable `DYNAMIC_DEBUG_CORE` and `DYNAMIC_DEBUG` to enable system-wide

### `DKMS`

Add this to `Kbuild` to enable dynamic debug for the module

```
ccflags-y := -DDYNAMIC_DEBUG_MODULE
```
