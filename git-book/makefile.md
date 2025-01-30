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

# Makefile

## Basic

```makefile
# Rule
targets: prerequisites
    command
    ...
```

## Variables

### Assignments

{% hint style="info" %}
Spaces at the end of a line are not stripped, but those at the start are
{% endhint %}

* `:=` Simple
* `+=` Append
* `?=` Only if not assigned yet
* `=` Recursive

#### Recursive variable example

```makefile
# Recursive variable. This will print "later" below
one = one ${later_variable}
# Simply expanded variable. This will not print "later" below
two := two ${later_variable}

later_variable = later

all: 
	echo $(one)
	echo $(two)
```

### Automatic variables

* `$@`: Target of the rule
* `$?`: All prerequisites newer than the target
* `$^`: All prerequisites
* `$<`: First prerequisite

```makefile
hey: one two
	# Outputs "hey", since this is the target name
	echo $@

	# Outputs "one" and/or "two" if they are newer than hey
	echo $?

	# Outputs "one two"
	echo $^
	
	# Outputs "one"
	echo $<
```
