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
---

# Poetry

{% embed url="https://realpython.com/dependency-management-python-poetry/#manage-dependencies-using-poetry" %}

## How to

### Show dependency tree

```
poetry show --tree [package]
```

### Compare current package versions to versions on PyPi

```
poetry show --latest --top-level
```
