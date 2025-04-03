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
pdsh -R ssh -w1900.{0..5} -w121.{0,1} sudo dmesg | grep bmcu
```

### Better output

Pipe pdsh into dshbak, the `-c` option avoids printing duplicate output

```bash
$ pdsh -w1906.{1,3,5} sudo erx-update-stm32 bmcu archive/BMCU-1.0.0.10.bin | dshbak -c
----------------
1906.[1,3,5]
----------------
Programming BMCU...
stm32flash 0.7

http://stm32flash.sourceforge.net/

Using Parser : Raw BINARY
Size         : 28136
Interface serial_posix: 57600 8E1
Version      : 0x31
Option 1     : 0x00
Option 2     : 0x00
Device ID    : 0x0466 (STM32G03xxx/04xxx)
- RAM        : Up to 8KiB  (4096b reserved by bootloader)
- Flash      : Up to 64KiB (size first sector: 1x2048)
- Option RAM : 128b
- System RAM : 8KiB
Write to memory
Erasing memory
Wrote and verified address 0x08006de8 (100.00%) Done.

Done
Reset the system as soon as possible!
```
