---
description: Handle dotfiles in wit git
---

# Chezmoi

## Terms

<table><thead><tr><th width="100"></th><th></th></tr></thead><tbody><tr><td>Source directory</td><td>Where the local git repo is (<code>chezmoi cd</code> to access it)</td></tr><tr><td>Source state</td><td>The state of the files in the source directory</td></tr><tr><td>Target</td><td>A file (usually a dotfile) you want to manipulate</td></tr></tbody></table>

[https://www.chezmoi.io/](https://www.chezmoi.io/)

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

## `chezmoi` ...

### `status`

First column: Diff between what chezmoi has and the actual state

Second column: Diff between actual state and the target state, and the effect of `chezmoi apply`

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

## How to

### Start synchronizing with repo

```
chezmoi init --apply git@github.com/pedrudehuere/dotfiles
```
