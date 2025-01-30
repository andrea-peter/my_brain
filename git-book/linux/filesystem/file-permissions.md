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

# File permissions

## Precedence

User > Group > Others

Example:

```
----r--rw- 1 abhi itsfoss 457 Aug 10 11:55 agatha.txt
```

`abhi` is part of the group `itsfoss`, but if he tries to do `cat agatha.rxt` he won't be able, but a user other than `abhi` that is part of the group `itsfoss` can read the file.

## Special permissions

### Numeric representation

* SUID = 4
* SGID = 2
* Sticky = 1

```
chmod n### <file>
```

### SUID (user + s)

* File exected as user who owns of file

### SGID (group + s)

#### On a file

* File executed as the **group** that owns the file

#### On a directory

* Any files created in the directory will have **group** ownership set to that of the directory owner

### Sticky (others + t)

#### On a directory

* Only owner (and root) of a file can delete file inside such a directory

