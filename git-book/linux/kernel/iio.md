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

# IIO

## Links

* [https://www.kernel.org/doc/html/v5.11/driver-api/iio/index.html](https://www.kernel.org/doc/html/v5.11/driver-api/iio/index.html)
* In kernel sources: Documentation/ABI/testing/sysfs-bus-iio

<figure><img src="../../.gitbook/assets/iio.drawio (2).png" alt=""><figcaption><p>IIO</p></figcaption></figure>

## Channel mode

* Direct: read/write when requested (e.g. via sysfs), the simplest one
* Various buffered modes
* Event triggered
* Hardware triggered

## sysfs

Files in `sysfs`  are automatically created according to:

* `channel.type`
* `channel.extended_name`
* `channel.output`
* ...

### Directory

`/sys/bus/iio/devices/iio:device<N>/`

### Filename

For raw values:Directory

`{in|out}_{type}_{extended_name}_raw`



***

Diagram sources:

{% file src="../../.gitbook/assets/iio (1).drawio" %}
