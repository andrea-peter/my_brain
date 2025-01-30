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

# udev

* `man udev`
* `man systemd-udevd`reacts to kernel event and calls and executes matching instructions specified in the udev sules

## Rules

* Located in `/etc/udev/rules.d`, `/lib/udev/rules.d` and others (see manual)
* Define what happens when a device is detected (plugged in)
* Executed when <mark style="color:red;">**... TODO**</mark>

## Utils

### udevadm

#### Reload rules

```
sudo udevadm control --reload-rules
```

#### Set log level to debug

```
sudo udevadm control --log-priority=debug
```

#### Get info about a device

With the `--attribute-walk` option parents are checked as well

```
$ udevadm info /dev/rtc0
P: /devices/platform/bpmp/bpmp:i2c/i2c-4/4-003c/nvvrs-pseq-rtc/rtc/rtc0
N: rtc0
L: -100
S: rtc
E: DEVPATH=/devices/platform/bpmp/bpmp:i2c/i2c-4/4-003c/nvvrs-pseq-rtc/rtc/rtc0
E: DEVNAME=/dev/rtc0
E: MAJOR=249
E: MINOR=0
E: SUBSYSTEM=rtc
E: USEC_INITIALIZED=13175431
E: DEVLINKS=/dev/rtc
```

For a walk along the parent devices

```
$ udevadm info /dev/rtc0 -a
```
