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

# Partitions

## How to

### See partitions and their UUID

```bash
sudo blkid
```

### See size in Bytes of a partition

```bash
sudo parted /dev/<partition> unit B p
```
