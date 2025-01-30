# sudo

## sudoers file

The file `/etc/sudoers` defines who can use `sudo` and how, to modify the file issue the command `visudo`.

```
man sudoers
```

## Configuration

* Configuration of `sudo` (including which plugins to load) resides in `/etc/sudo.conf`&#x20;
* The `sudoers` plugin is used by default if no Plugin lines are present
