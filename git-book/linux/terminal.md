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

# Terminal

## Terminfo

Database describing terminal emulator capabilities, see: [https://tldp.org/HOWTO/Text-Terminal-HOWTO-16.html](https://tldp.org/HOWTO/Text-Terminal-HOWTO-16.html)

For example, the package kitty-terminfo contains the file `/usr/share/terminfo/x/xterm-kitty` that describes the capabilities of the kitty terminal emulator

Terminfo files are compiled with the `tic` utility, compiled formats include `terminfo` and `termcap`

## Environment variables

### TERM

### TERMINFO

