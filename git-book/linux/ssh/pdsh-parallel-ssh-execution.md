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

# pdsh - parallel ssh execution

Execute commands via ssh in parallel

## Examples

### Check kernel messages on all 1900 and 121 nodes

```sh
pdsh -w1900.{0..5} -w121.{0,1} sudo dmesg | grep bmcu
```
