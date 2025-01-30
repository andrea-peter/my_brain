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

# Lua

[https://neovim.io/doc/user/lua.html](https://neovim.io/doc/user/lua.html)

### APIs

[https://neovim.io/doc/user/lua-guide.html#lua-guide-api](https://neovim.io/doc/user/lua-guide.html#lua-guide-api)

* VIM API
  * Ex-commands: `vim.cmd()`
  * builtin-commands: \<either the above or belove)
  * user-functions: `vim.fn`
* Nvim API, accessed through `vim.api`
* Lua API

### Entry point

Entry point, either of:

```
~/.config/nvim/init.lua
~/.config/nvim/init.nvim
```

## Vim commands

`vim.cmd`

```lua
vim.cmd("%s/\\Vfoo/bar/g")
```

```lua
vim.cmd([[
  highlight Error guibg=red
  highlight link Warning Error
]])
```

## Vimscript function

`vim.fn`, this works for both builtin-functions and user-functions

```lua
print(vim.fn.printf('Hello from %s', 'Lua'))
```

