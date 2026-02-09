---
description: iptables
---

# nftables

[https://wiki.archlinux.org/title/Nftables](https://wiki.archlinux.org/title/Nftables)

The Linux kernel subsystem is known as nf\_tables, ‘nf’ stands for Netfilter

Tables contain chains that contain rules

## Tables

Contain chains, no predefined tables (unlike _iptables_), they have a **name** and **family-type:**

* ip: IPv4 (usually the default if not specified)
* ip6: IPv6
* inet: both the above
* arp
* bridge
* netdev

```bash
nft list tables [FAMILY]
nft add table FAMILY TABLE_NAME
nft delete table FAMILY TABLE_NAME
nft flush table FAMILY TABLE_NAME
```

## Chains

Contain rules, no predefined chains (unlike _iptables_)

* **base chain**: entry point for packets on a network stack, a [hook](https://wiki.nftables.org/wiki-nftables/index.php/Netfilter_hooks) must be specified
* **regular chain**: may be used as jump target, used for better organization

Three types of chain:

* **filter**: Standard chain type to use when in doubt
* **nat**: For address translation
* **route**: For routing

```bash
nft list chains FAMILY
# Create base chain
nft add chain FAMILY TABLE_NAME CHAIN_NAME '{ type CHAIN_TYPE hook HOOK_TYPE priority PRIOTIY_VALUE ; policy POLICY ;}'
# Create regular chain
nft add chain FAMILY TABLE_NAME CHAIN_NAME
nft delete chain FAMILY TABLE_NAME CHAIN_NAME
nft flush chain FAMILY TABLE_NAME CHAIN_NAME
```

## Rules

```bash
nft list table FAMILY TABLE_NAME
nft list ruleset [family]
nft add rule FAMILY TABLE_NAME CHAIN_NAME [handle HANDLE_VALUE] STATEMENT
```

## How to

### Set-up Masquerading NAT

To allow a target board to access internet through host PC

[https://docs.redhat.com/en/documentation/red\_hat\_enterprise\_linux/7/html/security\_guide/sec-configuring\_nat\_using\_nftables#sec-Configuring\_masquerading\_using\_nftables](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/security_guide/sec-configuring_nat_using_nftables#sec-Configuring_masquerading_using_nftables)





