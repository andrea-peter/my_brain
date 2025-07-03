# Archives

## How to extract

#### .tgz, .tar.gz

```
tar -xzf archive.tbz -C /path/to/destination
```

#### .tzb, .tar.bz

```
tar -xjf archive.tbz -C /path/to/destination
```

## Multi-processing

### gzip

```
tar --use-compress-program=pigz -xf archive.tgz
```
