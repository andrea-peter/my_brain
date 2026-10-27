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
  anchors:
    visible: true
---

# Screen

## How to

<div align="left"><figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption><p>Mini cheat sheet</p></figcaption></figure></div>

### Detach

```
Ctrl+A
d
```

### Kill a window

```
Ctrl+A
k
```

## List windows

```
screen -ls
```

### Name window

Open window with name (name can be used for later screen commands instead of number)

```
screen -S <name>
```

## Reattach

```
screen -r <n|name>
```

### Scroll

```
Ctrl-a
Esc
```

Then `page-up`, `page-down`

### Pass CTRL-A to child process

{% code overflow="wrap" %}
```
Ctrl-a a
```
{% endcode %}
