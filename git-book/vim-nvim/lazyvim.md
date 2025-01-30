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

# Lazyvim

## Intro

* lazy.nvim: Plugin manager plugin for neovim
* LazyVim: Configuration of neovim with nice defaults (including lazy.nvim)

## Example config

```
~/.config/nvim/lua/plugins/example.lua
```

## Paths

```bash
~/.local/share/nvim/lazy   # Plugins installed by lazy vim
~/.local/share/nvim/mason  # Plugins installed by Mason
```

## Plugins

### Plugin categories

* Pre-installed
* Lazy-extras
* Third party

### Third party plugins

Create a lua file in the `plugins` folder, this lua module must return a table which the first element is the github name of the repo (`user/repo-name`), e.g:

```lua
return {
  "nmac427/guess-indent.nvim",
  opts = {
    auto_cmd = true,
    override_editorconfig = true
  },
  keys = {}
}
```

#### opts

The options specified in `opts` are passed to the `setup()` function of the plugin

#### keys

These are not passed to the plugin, rather, thery are parsed by the `Lazy.nvim` plugin manager

## Commands

* `LazyFormatInfo`

## Specifiv LazyVim things

### Space mode

This is specific to LazyVim

### Command mode navigation

{% hint style="danger" %}
Not sure if this is specific to LazyVim or to neovim
{% endhint %}

[https://lazyvim-ambitious-devs.phillips.codes/course/chapter-2/#\_command\_mode](https://lazyvim-ambitious-devs.phillips.codes/course/chapter-2/#_command_mode)

## Links

* [https://www.lazyvim.org/](https://www.lazyvim.org/)
* [https://lazyvim-ambitious-devs.phillips.codes/](https://lazyvim-ambitious-devs.phillips.codes/)

