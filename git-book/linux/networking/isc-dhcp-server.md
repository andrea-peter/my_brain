# isc-dhcp-server

DHCP server from the [Internet Systems Consortium](https://www.isc.org/dhcp/)

## Configuration

By default in `/etc/dhcp/dhcpd.conf`

Example config for the network `192.168.1/24` with an address pool of only the address `192.168.1.32`

```
subnet 192.168.1.1 netmask 255.255.255.0 {
  range 192.168.1.32 192.168.1.32;
}
```

## Leases

Assigned IP address (a.k.a leases) are stored in a file

## Command examples

Start dhcpd (IPv4) in foreground with given config and leases file

```
sudo dhcpd -4 -f -cf /home/andrea/dhcpd.conf -lf /home/andrea/dhcpd.leases
```



## Packages

* isc-dhcp-server
