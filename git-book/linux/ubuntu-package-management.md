# Ubuntu package management

## How to

### List files in a package

#### Installed package

```bash
dpkg-query -L <package-name>
```

#### .deb file

```bash
dpkg-deb -c <package-name>
```

#### Not installed package

```bash
apt-file list <package-name>
```
