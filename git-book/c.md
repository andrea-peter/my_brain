# C

## Const

Compiler ensures some things are not changed

### Const value

* Cannot change value

```c
const int const_num = 1;

const_num = 2;  // <-- error: assignment of read-only variable ‘const_num’
```

### Const pointer

* Cannot re-assign pointer
* Can change value through dereference

```c
int num = 1;
int * const const_ptr = & num;

// Not allowed to re-assign pointer
const_ptr = &other_num;  // <-- error: assignment of read-only variable ‘const_ptr’

// Allowed to change value through dereference
*const_ptr = 2;
```

### Pointer to const

* Can re-assign pointer
* Cannot change value through dereference

```c
int num = 1;
int other_num = 10;

int const * ptr_to_const = &num;
// FYI: int const can also be written as const int

// Allowed to re-assign pointer
ptr_to_const = &other_num;

// Not allowed to change the value pointed to by the pointer
*ptr_to_const = 11;  // <-- error: assignment of read-only location ‘*ptr_to_const’

// Allowed to change value when not going through pointer
other_num  = 11;
```

### In parameters

The same applies to function parameters, here the function guarantees that the content of the string is not modified

```c
 void print_string(const char* string) {
     // Declaring string as a pointer to const ensures that the value pointed to by string
     // is never modified, so the user can pass the pointer without worrying
     printf("String: \"%s\"\n", string);
 
     // Not allowed to do this
     // string[0] = 0x00;
 }
```

## Copy string

```
char* strcpy(char* destination, const char* source);
```

## Print errors

```
err.h
```

<table><thead><tr><th width="125">Function</th><th width="150">Append strerror</th><th>Exit program</th></tr></thead><tbody><tr><td>err</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>errx</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>warn</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td></td></tr><tr><td>warnx</td><td></td><td></td></tr></tbody></table>

`v<func>` versions of these functions exist

## Functions taking `va_list`

Sometimes functions that take a variable number of arguments, like

```c
void errx(int eval, const char *fmt, ...);
```

exist with a variant `v<func>` that takes a `va_list` as last argument instead `...`

`errx` can be called  like this

```c
errx(EXIT_FAIL, "Expected %zd items, got %zd", nb_expected, nb_items);
```

Let's say we want to encapsulate the call to `errx` because we need to free a resource before exiting (`err` exits the program). It would be cumbersome to pop the variable arguments from the stack just to pass them to `err`, this is why the function `verrx` exists which takes an argument of type `va_list` (`starg.h`) instead of `...`

```c
void verrx(int eval, const char *fmt, va_list args);
```

So our function might look something like this

```c
static void close_and_err(nfc_device *device, char *msg, int retval, va_list args) {
    nfc_close(device);
    verrx(retval, msg, args);
}
```

## Clearing buffers

#### stdout and stderr

stdout and stderr can be cleared with&#x20;

```c
fflush(stdout)
```

&#x20;and

```c
flush(stderr)
```

#### stdin

{% hint style="warning" %}
stdint **must not** be cleared with `fflush` since that causes undefined behaviour according to the standard
{% endhint %}

