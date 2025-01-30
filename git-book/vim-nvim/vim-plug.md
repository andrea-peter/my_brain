---
layout:
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
---

# vim-plug

[vim-plug](https://github.com/junegunn/vim-plug) is a minimalist plugin manager for vim

List the plugins to install in `.vimrc`, then execute `:PlugInstall` to install them

## &#x20;Commands

| `PlugInstall [name ...] [#threads]` | Install plugins                                                   |
| ----------------------------------- | ----------------------------------------------------------------- |
| `PlugUpdate [name ...] [#threads]`  | Install or update plugins                                         |
| `PlugClean[!]`                      | Remove unlisted plugins (bang version will clean without prompt)  |
| `PlugUpgrade`                       | Upgrade vim-plug itself                                           |
| `PlugStatus`                        | Check the status of plugins                                       |
| `PlugDiff`                          | Examine changes from the previous update and the pending changes  |
| `PlugSnapshot[!] [output path]`     | Generate script for restoring the current snapshot of the plugins |
