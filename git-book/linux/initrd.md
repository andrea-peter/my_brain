# initrd

Normally a gzipped cpio archive

## How to

### Extract

{% hint style="danger" %}
As root in order to preserve file ownership
{% endhint %}

For gzip

```
zcat initrd | cpio -idmv
```

or

```
unmkinitramfs initrd extracted_initrd/
```

For LZMA (untested)

```
xz -dc < /boot/initrd-$(uname -r).img | cpio -idmv
```

### Repack

For gzip (untested)

```
find extracted_initrd/ | cpio -o -c -R root:root | gzip -9 > new_initrd
```

For LZMA (untested)

{% code overflow="wrap" %}
```
find extracted_initrd/ 2>/dev/null | cpio -o -c -R root:root | xz -9 --format=lzma > new_initrd
```
{% endcode %}
