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

# Users and groups

## Groups

There are primary and secondary groups

#### Primary group

A group that the OS assigns to files that the user creates, each user must belong to a primary group

#### Secondary group

One or more groups to which a user also belongs, users can belong to serveral secondary groups

## /etc/group

```
group name
 |    password field (not used)
 |     | group id (GID)
 |     |  |   list of users belonging to this group
 |     |  |    |
andrea:x:1000:
```

## /etc/passwd

```
user nameqq
 |    password field (not used)
 |     | user ID (UID)
  |     |  |  primary-group ID
  |     |  |    |             home directory
  |     |  |    |              | 
andrea:x:1000:1000:Andrea,,,:/home/andrea:/bin/bash
```

## How to

#### Chane user's shell

```
sudo usermod --shell /bin/bash USERNAME
```
