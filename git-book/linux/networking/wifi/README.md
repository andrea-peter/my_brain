# Wifi

## How to

#### List wifi interfaces

```
iwconfig
```

#### List available wifis

<pre><code><strong>sudo iwlist &#x3C;iface> scan | grep SSID
</strong></code></pre>

#### Configure to connect to wifi

Edit the file `/etc/wpa_supplicant/wpa_supplicant.conf` to contain

```
network={
  ssid="SSID"
  psk="WIFI PASSWORD"
}
```

##
