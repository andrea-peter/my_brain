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

# IP command

## Tips and tricks

* Alias the `ip` command to `ip -color=auto` to have colors when output goes to a tty

## How to

### List interfaces

```
ip link show
```

### Display current settings

```
ip address show dev IFNAME
```

### Add IP address on interface (my be temporary according to running services)

```
ip address add dev IFNAME <address>/<network-suffix> brd +
```

### Default gateway

#### List

```
ip route list default
```

#### Delete

```
ip route delete default
```

#### Set

```
ip route add default via IP dev IFNAME
```

### Clear IP settings of an interface

```
ip address flush dev IFNAME
```
