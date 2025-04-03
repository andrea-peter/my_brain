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

# Shells

[https://www.linuxquestions.org/questions/linux-general-1/difference-between-normal-shell-and-login-shell-14983/#post4828786](https://www.linuxquestions.org/questions/linux-general-1/difference-between-normal-shell-and-login-shell-14983/#post4828786)

**Interactive:** As the term implies: Interactive means that the commands are run with user-interaction from keyboard. E.g. the shell can prompt the user to enter input.

**Non-interactive:** the shell is probably run from an automated process so it can't assume it can request input or that someone will see the output. E.g., maybe it is best to write output to a log file.

**Login:** Means that the shell is run as part of the login of the user to the system. Typically used to do any configuration that a user needs/wants to establish his work environment.

**Non-login:** Any other shell run by the user after logging on, or which is run by any automated process which is not coupled to a logged in user.

## Init scripts

Login shell calls `.profile`  which in turn calls `.bashrc`

Interactive shell calls only `.bashrc`

## How to know

### Login shell

```
$ echo $0
-bash
```

* -bash = login shell
* bash = not login

### Interactive shell

```
$ [ -t 0 ] && echo stdin is a tty
$ [ -t 1 ] && echo stdout is a tty
```

The $- env var tells you what options your shell runs in. i=interactive

```
$ echo $-
himBH
```
