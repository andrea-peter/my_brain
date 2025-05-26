# vim/nvim



## Buffers

### Load files

#### `:e[dit] <filename>`

Load given file in the current buffer, replace current loaded file if any

#### `:bad[d]` or :`bad <filename>`

Buffer-add, add the given file to a new buffer

### Close buffers

#### `:bd[elete] <filename|index>`&#x20;

Close buffer of given file name or index

### List open buffers

#### `:ls` or `:files` or `:buffers`&#x20;

Each open buffer can have these flags:

* `%` : Buffer which is in the current window
* `#` : Alternate buffer (the last file which was most recently edited in the current window)
* `a` : Active buffer (the file which is being edited in the current window)
* `h` : Hidden buffer (buffer with unsaved modifications but is not being displayed in any window)
* `u` : Unlisted buffer (files that are not open in Vim but are present in the current working directory; use `:ls!` to view this)
* `-` : Buffer with 'modifiable' set to off
* `=` : A read-only buffer
* `+` : A modified buffer (buffer with changes that are not written to disk)
* `x` : A buffer that has read errors

### Switch to buffer

#### `:b[uffer] <filename|index>`

Switch to given buffer in current window

## Clipboards

##

## Commands

#### `:help`

Print help of settings or commands

#### `:<m>map` and `:<m>noremap`&#x20;

Recursive and non-recursive map, map `{lhs}` command to `{rhs}` when the mode `<m>` applies. See `:help map-overview` for the different modes.

## File types

```vim
:help filetype
```

Get current file ype

```vim
:set filetype?
```

Set current file type

```vim
:set filetype=systemd
```

Try to detect file type

```vim
:filetype detect
```

## Indentation settings

[https://gist.github.com/LunarLambda/4c444238fb364509b72cfb891979f1dd](https://gist.github.com/LunarLambda/4c444238fb364509b72cfb891979f1dd)



## Marks

`:help marks`

* \[a-z]: Local to files
* \[A-Z]: Global

### Commands

* `mC`: Create `C` mark
* `'C`: Navigate to `C` mark
* `marks`: List all marks
* `marks {marks}`: List mentioned marks
* `delm[arks] {marks}` : delete marks

## Navigate files

#### `Ex[plore] [<path>]`

Open folder at path or folder of current file, if current file contains unsaved changes the window is split. Similar command with a different prefix exist: `Explore`

## Options

```
help set-option
```

```
set             # Show all options that differ from default
set!            # One option per line
set {option}?   # Show value of option
set {option}    # Toogle option: set, number and string: show value
set no{option}  # Toogle option: clear
set {option}!   # Toggle option: toggle
set inv{option} #  idem
set {option}={value}   # Set value
set {option}:{value}   # idem

```

## Search

```
/<pattern>
```

#### Search for whole word

Enclose pattern with `\<` and `\>`

## Find and replace

In general, to search each line in `[range]` for a `{pattern}`, and replace it with a `{string}`.&#x20;

No range: current line

`[count]` is a positive integer that multiplies the command:

```
:[range]s/{pattern}/{string}/[flags] [count]
```

### Range

`from,to` - both inclusive

### Flags

* `c`: confirm each
* `g`: globally (not only the first occurrence)

### Examples

#### Replace on current line

Replace first occurrence of `foo` with `bar`

```
:s/foo/bar
```

All occurrences

```
:s/foo/bar/g
```

#### Replace in entire file

Use `%` as range

```
:%s/foo/bar/g
```

#### Delete

Omit `{string}`

```vi
:s/foo//g
```

#### Replace with newline

To replace with newline you must use `\r` (and not `\n`), see [https://vim.fandom.com/wiki/Search\_and\_replace#Details](https://vim.fandom.com/wiki/Search_and_replace#Details)

### Various

#### Alternative separator

You can use any non-alphanumeric single-byte character instead of `/` in case `/` is used in a pattern.

Example, replace `\` with `/`:

```
:s-\\-/-g
```

## Registers

```
:help registers
:dis    # Prints all register contents
```

* Unnamed `""`: Filled by commands `d`, `c`, `s`, `x`, `y`, used to fille by command  `p` if no register is specified
* 10 numbered registers `"0` to `"9`:&#x20;
* Small delete register `"-`:
* Named registers `"a` to `"z` or `"A` to `"Z`:
* Read-only registers `":` `".` `"%`:
* Alternate file register `"#`:
* Expression register `"=`:
* Selection registers `"*` and `"+`:
* Black hole register `"_`:
* Last search register `"_`:

## Scrolling

### Scrolling without moving cursor

* `z` `z`: Current line center of scree
* `z` `t`: Current line top of screen
* `z` `b`: Current line bottom of screen
* `Ctrl` + `y`: Move up one line
* `Ctrl` + `e`: Move up one line
* `z` `h`/`H`: Scroll left
* `z` `l`/`L`: Scroll right

```
+-------------------------------+
^                               |
|c-e (keep cursor)              |
|H(igh)             zt (top)    |
|                   ^           |
|           ze      |      zs   |
|M(iddle)  zh/zH <--zz--> zl/zL |
|                   |           |
|                   v           |
|L(ow)              zb (bottom) |
|c-y (keep cursor)              |
v                               |
+-------------------------------+
```

## Windows

Several buffers can be displayed simultaneously

### Split

* Horizontally: `:split`
* Vertically: `:vsplit` or `CTRL` `V`

### Open all buffers in separate windows

* `:ball`&#x20;
* `:vertical ball`

### Navigate

* Jump to window,`CTRL`+ one of: `h`, `j`, `k`, `l`

### Resize

Increase/decrease by `<n>` rows/columns, 1 by default

* Increase height `CTRL+W`, `<n>,` `+`
* Decrease height: `CTRL+W`, `<n>`, `-`
* Increase width: `CTRL+W`, `<n>`, `>`
* Decrease width: `CTRL+W`, `<n>`, `<`

## Tips and tricks

### Edit binary files

1. Open file in vim
2. Conver to textual representation: `:%!xxd`
3. Edit the file
4. Convert back to binary: `:%!xxd -r`
