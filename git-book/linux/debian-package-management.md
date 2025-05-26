# Debian package management

## How to

#### Search for a package

```
apt search <search-term>
```

#### List files in a package

```
dpkg-query -L <package-name>
```

#### Show status of package

```
dpkg-query --status <package-name>
```

#### Prevent package from being updated

```
echo <package> hold | dpkg --set-selection
```

to check

```
dpkg --get-selections
```

#### List content of a .deb file

```
dpkg-deb -c <mypackage.deb>
```

#### Se dependencies of a package

```
apt-cache depends <package-name>
```
