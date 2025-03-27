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

# Network manager

Based on concept of connection profiles (a.k.a connections), connection profiles are applied to devices when connections are activated

Base folder: `/etc/NetworkManager/`&#x20;

## nmcli - command line tool

Commands for `nmcli` can be shortened as long as the are unique (e.g. `nmcli connection show` can be shortened to `nmcli c s`)

### Connections

#### List connections

We can see here that there's no wifi connection

```
$ nmcli connection show
NAME                UUID                                  TYPE      DEVICE 
Wired connection 1  08143a8a-37bf-311b-bba0-e3986f6825c9  ethernet  eth0   
lo                  2ec8c8da-567e-4138-9d84-d2208fa9af39  loopback  lo
```

#### Activate connection

```
# nmcli connection up ifname wlan0

```

### Devices

#### List devices

We can see that there's a wifi device (without connection though)

```
$ nmcli device status
DEVICE  TYPE      STATE                   CONNECTION         
eth0    ethernet  connected               Wired connection 1 
lo      loopback  connected (externally)  lo                 
wlan0   wifi      unmanaged               --                 
```

#### Show details for device

```
$ nmcli device show wlan0
GENERAL.DEVICE:                         wlan0
GENERAL.TYPE:                           wifi
GENERAL.HWADDR:                         B8:27:EB:47:E9:C6
GENERAL.MTU:                            1500
GENERAL.STATE:                          10 (unmanaged)
...
```

## Example, create wifi connection

Ensure wifi radio is on

```
$ sudo nmcli radio wifi on
$ nmcli radio
WIFI-HW  WIFI     WWAN-HW  WWAN    
enabled  enabled  missing  enabled
```

Create connection

```
sudo nmcli connection add type wifi ifname wlan0 autoconnect yes save yes ssid RUT_18D7_2G
```



List available wifi devices

```
$ nmcli device wifi list
```

