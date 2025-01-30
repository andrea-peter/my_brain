---
description: Handle dotfiles in wit git
---

# Chezmoi



[https://www.chezmoi.io/](https://www.chezmoi.io/)

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

## `chezmoi` ...

### `status`

```
  Character     │Meaning       │First column           │Second column
  ──────────────┼──────────────┼───────────────────────┼──────────────────────────
  Space         │No change     │No change              │No change
  A             │Added         │Entry was created      │Entry will be created
  D             │Deleted       │Entry was deleted      │Entry will be deleted
  M             │Modified      │Entry was modified     │Entry will be modified
  R             │Run           │Not applicable         │Script will be run
```

### `diff`

Print the difference between the target state and the destination state for targets

### `forget`

Remove targets from the source state, i.e. stop managing them
