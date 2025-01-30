# Cross compiling

## Gen2

ornx has Ubuntu 22.04 with a custom nvidia kernel&#x20;

```bash
$ uname -a
Linux erxbot-121-0 5.10.120-tegra #1 SMP PREEMPT Wed Jun 12 18:17:09 UTC 2024 aarch64 aarch64 aarch64 GNU/Linux
```

## Prerequisites

```bash
sudo apt install gcc-11-aarch64-linux-gnu
```

\
Trying to get `/usr/lib/gcc/x86_64-linux-gnu/9` looks like we need to install `gcc9`

```bash
sudo apt install gcc-9
```
