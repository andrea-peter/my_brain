# Bash

## Completion

```
man bash  # section 'Programmable Completion'
```

```
help completion
```

### Files

```
/etc/bash_completion
/etc/bash_completion.d
```

&#x20;`/etc/bash_completion` normally points to something like `/usr/share/bash-completion/`, completions for commands are in the `completion/` folder.

### Command specific completions

Since every command can implement its own "add-my-custom-completion" framework, each command has its own sauce

#### git

The file `/usr/share/bash-completion/completions/git/` contains the function `__git_complete`, copy/source this file and use like this:

```
__git_complete <alias> <git-cmd>
```

e.g.

```
__git_complete gs git_status
```

## File name matching

Let the file system by like this

```
file1.a
file1.b
file1.c
file1.d
file2.a
```

#### Delete all files starting with `file1`

```
rm file1*
```

#### Delete `file1.a` and `file1.c`

```
rm file1.[ac]
```

#### Delete `file1.a` to `file1.c`

```
rm file1.[a-c]
```

## Previous commands

* `!$` - last argument from previous command
* `!^` - first argument (after the program/built-in/script) from previous command
* `!*` - all arguments from previous command
* `!!` - previous command (often pronounced "bang bang")
* `!n` - command number `n` from `history`
* `!pattern` - most recent command matching `pattern`
* `!!:s/find/replace` - last command, substitute `find` with `replace`

## Special parameters

* `$1`, `$2`, `$3` - are the positional parameters
* `"$@"` - is an array-like construct of all positional parameters, `{$1, $2, $3 ...}`.
* `"$*"` - is the IFS expansion of all positional parameters, `$1 $2 $3 ...`.
* `$#` - is the number of positional parameters.
* `$-` - current options set for the shell.
* `$$` - pid of the current shell (not subshell).
* `$_` - most recent parameter (or the abs path of the command to start the current shell immediately after startup).
* `$IFS` - is the (input) field separator.
* `$?` - is the most recent foreground pipeline exit status.
* `$!` - is the PID of the most recent background command.
* `$0` - is the name of the shell or shell script.

## Parameter expansion

[https://www.gnu.org/software/bash/manual/html\_node/Shell-Parameter-Expansion.html](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)

#### ${parameter:-word}

If `parameter` is unset or null the expansion of `word` is substituted (`word` can be an expansion), otherwise the value of `parameter` is substituted

```bash
$ echo ${var:-DEFAULT}
DEFAULT
$ var=miao
$ echo ${var:-DEFAULT}
miao
```

#### ${parameter:=word}

TODO

#### ${parameter:?word}

TODO

#### ${parameter:+word}

TODO

#### ${parameter:offset}

TODO

#### ${parameter:offset:length}

TODO

#### ${!parameter}

Indirect expansion

```bash
$ hello="this is some text"   # we set $hello
$ var="hello"                 # $var is "hello"
$ echo "${!var}"              # we print the variable linked by $var's content
this is some text

```

#### ${parameter%/}

#### ${parameter#word}

Pattern matching with **shortest** matching pattern deleted

#### ${parameter##word}

Pattern matching with **longest** matching pattern deleted



## Arrays

```bash
TEMPS=("inside" "outside")
TEMPS+=("CPU")
TEMPS+=("GPU")

```

## Arithmetic expansion

```bash
$ var=3
$ echo $((var+3))
6
```

```bash
$echo $((x=4,y=5,z=x*y,u=z/2))
10
$ echo $x $y $z $u
4 5 20 10
```

```bash
$ for i in {1..5}; do echo $i; done
1
2
3
4
5
```

```bash
END=5
for ((i=1;i<=END;i++)); do
    echo $i
done
```

<pre class="language-bash"><code class="lang-bash"><strong>$ i=1
</strong>$ ((i+=1))
$ echo $i
2
</code></pre>

## Built-in commands

### shopt

See/change shell optional behavior

## How to

### Execute commands in background from a loop

```
for n in {0..5}; do scp image.mender 1900.$n & done
```

### Show background tasks in session

```
jobs -l
```

## Links

* [Bash reference manual](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html)
