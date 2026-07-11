---
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# gpg

## List keys

```
gpg -k
```

## Create key

```
gpg --quick-generate-key --batch your@email.com
```

## Import key

```
gpg --import <the-key-file>
```

## Sign key

```
gpg --sign-keys <the-key-ID>
```

## Show fingerprint of key

```
gpg --ginderprint <the-key-ID>
```

## Verify signature

```
gpg --verfiy <signature.sig> <file-to-verify>
```
