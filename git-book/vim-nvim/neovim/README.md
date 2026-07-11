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

# Neovim

## Files and configs

### Standard paths

[https://practical.li/neovim/reference/neovim/standard-path/](https://practical.li/neovim/reference/neovim/standard-path/)

* **Config**: `~/.cache/nvim/`
* **Config**: `~/.config/nvim/`
  * User configs
* **Data**: `~/.local/share/nvim/`
  * Plugins
* **Run**: `/tmp/nvim.user/xxx/`
* **State**: `~/.local/state/nvim/`
  * Logs
  * Sessions
  * Undo data

### Where is[https://luals.github.io/wiki/annotations/](https://luals.github.io/wiki/annotations/)

* Mason packages: `<data-path>/mason`

## Mappings

See mappings

```
:map
```

## Registers mini-mode

In **INSERT** mode type `<C-R>`

## Do commands

Apply action to

* argdo: all arguments in the arglist
* bufdo: all buffers
* cdo: each valid entry in the quickfix list
* cfdo: each file in the quickfix list
* tabdo: all tabs
* windo: all windows

## Themes

{% hint style="danger" %}
Custom

`~/.config/nvim/lua/plugins/fscheme.lua`
{% endhint %}

## Autocmd

{% embed url="https://neovim.io/doc/user/autocmd.html" %}

* List autocommands:  `au[tocmd] [group] {event} {aupat}`

## Clipboard

## Directories

* Config directory: `~/.config/nvim`

### Log files

```
~/.local/share/nvim/neo-tree.nvim
~/.local/state/nvim/lsp.log
```

### History files

```
~/.local/share/nvim/telescope_history
```

## Plugins

{% tabs %}
{% tab title="Lazy.nvim" %}
<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Telescope" %}
<figure><img src="../../.gitbook/assets/plugin_telescope (5).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Neo-tree, Trouble" %}
<figure><img src="../../.gitbook/assets/plugins_neotree_trouble.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Noice" %}
<figure><img src="../../.gitbook/assets/plugin_noice.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Gitsigns" %}
<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="nvim-dap" %}
## Debugger

[https://github.com/mfussenegger/nvim-dap](https://github.com/mfussenegger/nvim-dap)

[https://github.com/mfussenegger/nvim-dap-python](https://github.com/mfussenegger/nvim-dap-python)

Virtualenv: put this in `.envrc`:

```
export VIRTUAL_ENV=$(pyenv prefix)
```

Launch debugger session with something like:

```
PYTHONPATH=src:tests python -m debugpy --listen 5678 --wait-for-client -m pytest -k test_config.py
```

then attach debugger in nvim
{% endtab %}
{% endtabs %}

### Lazy.nvim

[https://github.com/folke/lazy.nvim](https://github.com/folke/lazy.nvim)

Plugin manager

lualine

[https://github.com/nvim-lualine/lualine.nvim](https://github.com/nvim-lualine/lualine.nvim)

Status line at the bottom

### blink.cmp

Autocompleton with LSP support

[https://cmp.saghen.dev/](https://cmp.saghen.dev/)

### Trouble

[https://github.com/folke/trouble.nvim](https://github.com/folke/trouble.nvim)

A pretty list for showing diagnostics, references, telescope results, quickfix and location lists to help you solve all the trouble your code is causing.

### Neo-tree

[https://github.com/nvim-neo-tree/neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim)

Default config with comments: [https://github.com/nvim-neo-tree/neo-tree.nvim/blob/main/lua/neo-tree/defaults.lua](https://github.com/nvim-neo-tree/neo-tree.nvim/blob/main/lua/neo-tree/defaults.lua)

Type `?` for help, then `ESC` to close help dialog

### Telescope

[https://github.com/nvim-telescope/telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)

Fuzzy finder over lists

### Noice

[https://github.com/folke/noice.nvim](https://github.com/folke/noice.nvim)

[https://github.com/folke/noice.nvim/wiki/A-Guide-to-Messages](https://github.com/folke/noice.nvim/wiki/A-Guide-to-Messages)

Messages

### lsp-config

Contains pre-baked configs for many language servers

```vim
:help lspconfig-all
```

Print static config definition of a language server:

```vim
:lua print(vim.inspect(require'lspconfig'.bashls.config_def))
```

### jq

To format whole buffer: `:%!jq`

### Conform

[https://github.com/stevearc/conform.nvim](https://github.com/stevearc/conform.nvim)

Formatter

log file: `/home/andrea/.local/state/nvim/conform.log`

## Spell-check

```viml
help spell

" Set spelling for buffer
:setlocal spell spelllang=en_US
:setlocal spell spelllang=fr_FR

" Find misspelled words
[s
]s

" Get suggestions for missspelled word under/after cursor
z=

" Add word to spellfile
zg


```
