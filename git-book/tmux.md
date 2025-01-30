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

# tmux

```
session
  |
  +-- windows
```

## Configuration

```
# File: ~/.tmux.conf

# Allow scrolling with mouse
set -g mouse on
```

## How to

### Sessions

#### New session

```
tmux new -s <session-name>
```

#### Attach session

```
tmux attach-session -t <session-name>
```

## Scripting

Example to (re)create a session

```bash
#!/bin/zsh                                                                                                   

SESSIONNAME="script"
tmux has-session -t $SESSIONNAME &> /dev/null

if [ $? != 0 ] 
 then
    tmux new-session -s $SESSIONNAME -n script -d
    tmux send-keys -t $SESSIONNAME "~/bin/script" C-m 
fi

tmux attach -t $SESSIONNAME
```

## Keymap

`Ctrl` + `B` then... (lowercase)

#### Sessions

* `S`: List
* `$`: Rename
* `D`: Detach
* `?`: Display help

#### **Windows**

* `C`: Create new
* `,`: Rename
* `W`: List
* `X`: Kill window
* `N`: Next window
* `P`: Previous window
* `0`-`9`: Display window with number

#### Panes

* `Q`: Show pane numbers
* `"`: Split horizontally
* `%`: Split Vertically
* `O`: Cycle through panes
* `{`: Swap position with previous
* `}`: Swap position with next
* `X`: Close current

To resize a pane keep `Ctrl` + `B` pressed and then either of the arrow keys

## Automation with `tmuxinator`

See [https://github.com/tmuxinator/tmuxinator/tree/v1.1.4?tab=readme-ov-file#usage](https://github.com/tmuxinator/tmuxinator/tree/v1.1.4?tab=readme-ov-file#usage)

Create a project

```bash
tmuxinator new [--local] [project-name]
```

* `--local` will create the project in the current dir instead of `~/.config/tmuxinator`

## Automatically save and restore sessions

[https://github.com/tmux-plugins/tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect)

