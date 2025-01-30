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

# Filesystem

{% hint style="warning" %}
`LABEL` != `PARTLABEL`\
[https://superuser.com/questions/1099232/what-is-the-difference-between-a-partition-name-and-a-partition-label](https://superuser.com/questions/1099232/what-is-the-difference-between-a-partition-name-and-a-partition-label)
{% endhint %}



## Watch files

### Prerequisites

```
sudo apt install inotify-tools
```

```
while inotifywait DIR; do CMD; done
```

## Utilities

### df

Filesystem disk usage

The `-B` option allows to specify a number format (Megabytes in the example)

```sh
$ df -BM
Filesystem     1K-blocks     Used Available Use% Mounted on
tmpfs            3994796     2292   3992504   1% /run
/dev/nvme0n1p2 982862268 81851516 851010420   9% /
tmpfs           19973960   341776  19632184   2% /dev/shm
tmpfs               5120        4      5116   1% /run/lock
efivarfs             248       65       179  27% /sys/firmware/efi/efivars
/dev/nvme0n1p1    523248     6220    517028   2% /boot/efi
tmpfs            3994792     1728   3993064   1% /run/user/1000
```

### du

Files and directories disk usage

### lsblk

List block devices

<pre><code>lsblk
<strong>lsblk -o name,mountpoint,partlabel,size,uuid
</strong></code></pre>
