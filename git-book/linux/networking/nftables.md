---
description: iptables
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

# nftables

The Linux kernel subsystem is known as nf\_tables, and ‘nf’ stands for Netfilter

Tables contain chains that contain rules

## Tables

Container of chaings, tables have a **name** and an **address family:**

* ip: IPv4
* ip6: IPv6
* inet: both the above
* arp
* bridge
* netdev

## Chains

Containers of rules: **base chains** (entry point for packets on a network stack) and **regular chains(m**ay be used as jump target, used for better organisation)

Three types of chain:

* **filter**: Standard chain type to use when in doupt
* **nat**: For address translation
* **route**: For routing

## Rules

## How to

### List rules

```
sudo nft list ruleset [family]
```

### List existing tables

```
sudo nft list tables [family]
```

```
$ sudo nft list tables
table ip nat
table ip filter
      |   |
      |   +--- Name
      +--- Address family
```

There are two tables, `nat` and `filter`, both with address family `ip`

### List chains and rules in a table

```
sudo nft list table [family] NAME
```

```
$ sudo nft list table ip nat
table ip nat {
	chain DOCKER {
		iifname "docker0" counter packets 0 bytes 0 return
	}

	chain POSTROUTING {
		type nat hook postrouting priority srcnat; policy accept;
		oifname != "docker0" ip saddr 172.17.0.0/16 counter packets 0 bytes 0 masquerade 
	}

	chain PREROUTING {
		type nat hook prerouting priority dstnat; policy accept;
		fib daddr type local counter packets 2893 bytes 517935 jump DOCKER
	}

	chain OUTPUT {
		type nat hook output priority -100; policy accept;
		ip daddr != 127.0.0.0/8 fib daddr type local counter packets 4 bytes 240 jump DOCKER
	}
}

```
