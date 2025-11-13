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

`man passwd`

```
user name
 |    password field (not used)
 |     | user ID (UID)
 |     |  |  primary-group ID
 |     |  |    |             home directory
 |     |  |    |              | 
andrea:x:1000:1000:Andrea,,,:/home/andrea:/bin/bash
```

## /etc/shadow

`man shadow`

Contains information about users.

The password field contains either:

* Hashed password (`$<nb><salt><hashed-passwd`), where nb indiateds the  hashing algorithm
* `!`: Locked, cannot login with password authentication
* !!: User created without password, cannot login with password authentication
* `*`: Cannot login with password authentication (e.g. for daemon)



## How to

#### Chane user's shell

```
sudo usermod --shell /bin/bash USERNAME
```
