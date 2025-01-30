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

# systemd

[https://wiki.archlinux.org/title/Systemd](https://wiki.archlinux.org/title/Systemd)

* Largely compatible with SysV init scripts

## Units

{% hint style="info" %}
`man systemd.unit`
{% endhint %}

* 11 different types
* Named as their configuration file
* Dependencies between units (requires/conflicts, before/after)

### Unit name

```
name-prefix.unit-type
```

The name-prefix can be parametrized with an instance name (e.g. with a counter) lile:

```
unit-name@instance-name.unit-type
```

### Unit files

* Plain text ini-style
* Loaded from a set of paths

#### List units

```bash
systemctl list-units [--all]
```

```bash
systemctl list-unit-files PATTERN
```

Example:

```bash
systemctl list-unit-files '*dhcp*'
```

```
systemctl start|stop|restart|reload|status <service>
```

### Show unit file content

```
systemctl cat <unit>
```

### Enable/disable unit

```bash
systemctl enable|disable UNIT
```

### Mask/unmask unit

```bash
systemctl mask|unmask UNIT
```

### Override unit options without overriding upstream file

This will create a file in `/etc/systemd/system/unit.d` (or similar)

```
systemctl edit [--full] UNIT
```

## Timers

### How to

#### See timers

```bash
systemctl list-timers [--all]
```

#### Validate times

```bash
$ systemd-analyze timespan "2h"
Original: 2h        
      μs: 7200000000
   Human: 2h
```

```bash
$ systemd-analyze calendar '*-*-* *:*:00'
Normalized form: *-*-* *:*:00                
    Next elapse: Tue 2024-04-09 10:51:00 CEST
       (in UTC): Tue 2024-04-09 08:51:00 UTC 
       From now: 45s left
```

## Logs

Logs can be queried with the `journalctl` command

### Query logs

#### Since a certain time

```
journalctl --since '2 minutes ago'
```

#### For a specific boot

```
journalctl --boot  # current boot
```

```
journalctl --boot=<boot-id>  # a specific boot
```

#### For a certain unit

```
journalctl -u 'some_prefix*'
```

## Common units

* `systemd-udevd.service`: Launched on udev events &#x20;

