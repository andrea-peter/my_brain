# AppArmor



## Profiles

Profiles in `/etc/apparmor.d`, each file corresponds to an executable, by convention the filename is the path with `.` instead of `/`.

### Complain mode

Profile violations are permitted and logged. Useful for testing and developing new profiles.

### Enforce mode

Enforces profile policy as well as logging the violation.

## Commands

#### aa-complain /path/to/bin

Put a profile (executable) in complain mode, a profile file is automatically created if it does not exist

```
sudo aa-complain /usr/sbin/dhcpd
```

#### aa-enforce /path/to/bin

Put a profile in enforce mode

#### apparmor\_parser

Load (or realod with `-r)` a profile into the kernel

```
sudo apparmor_parser -r /etc/apparmor.d/profile.name
```

#### apparmor\_status

Print status of apparmor and profiles

#### systemctl reload apparmor.service

Reload all profiles

## Packets

* apparmor-profiles
* apparmor-utils

## Links

* [Ubuntu AppArmor doc page](https://ubuntu.com/server/docs/security-apparmor)
