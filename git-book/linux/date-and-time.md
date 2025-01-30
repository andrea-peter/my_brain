# Date and time

## System time

#### Print date in filename format

```
date +%Y%m%d%H%M%S
```

#### Set date

```
sudo date --set "18 Apr 2024 14:53:00"
```

## Hardware clock

#### Show hardware clock time

```
sudo hwclock
sudo hwclock --rtc=/dev/rtc1
```

## Hardware to/from system clock

#### Set system time to hardware clock

```
sudo hwclock --systohc
```

#### Set hardware clock to system time

```
sudo hwclock --hctosys
```

## Kernel configuration

* `CONFIG_RTC_SYSTOHC`: Whether to update (every \~11 mins) RTC’s time with system time when system time is synced (RTC device defined by CONFIG\_RTC\_HCTOSYS\_DEVICE)
* `CONFIG_RTC_HCTOSYS_DEVICE`: To which RTC to write system time - e.g: `RTC0`
* `CONFIG_RTC_HCTOSYS`: Whether to set system time from RTC on boot
* `CONFIG_RTC_HCTOSYS_DEVICE`: Which RTC to use to set system time on boot - e.g: `RTC0`

### Periodic system time writeback to RTC

if the kernel has been compiled with `CONFIG_RTC_SYSTOHC` and the system time is being kept up to date by an NTP client, the kernel updates the hardware clock automatically every \~11 minutes

#### How does the kernel know whether the system clock is being synchronised?

The kernel variable `time_status` (not to be confused with the variable `time_state`) contains clock status flags, he flag `STA_UNSYNC` is set by default and cleared when the clock is synchronised

```c
//file: timex.h
#define STA_UNSYNC	0x0040
```

The command `adjtimex` allows to see (`--print`) and set (`--status STATUS`) this variable

A human friendly way to check this:

{% code overflow="wrap" %}
```bash
[ $(( $(adjtimex -p | grep 'status: ' | tr -s ' '| cut -d' ' -f3) & 64)) -eq 64 ] && echo 'System clock NOT synced' || echo 'System clock synched'
```
{% endcode %}

## timedatectl and systemd-timedated

```
man timedatectl
man systemd-timedated
```

{% hint style="danger" %}
Not to be confsed with`systemd-timesyncd`
{% endhint %}

`timedatectl` is the CLI client for the service `systemd-timesyncd`, the service can be used to access some basic time settings

## systemd-timesyncd

NTP client by `systemd`

