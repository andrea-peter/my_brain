---
description: Limit shell resource utilization
---

# ulimit

## Soft vs hard limits

* Hard limit: maximum permitted, set by admin
* Soft limit: Set by user, cannot exceed hard limit

## List all current limits

```
ulimit -a
```

## Set core dump limit

* Soft: 1 MB
* Hard: 10MB

```
sudo prlimit --pid $$ --core=1048576:10485760
```
