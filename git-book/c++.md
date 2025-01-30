# C++

## Examples

Here are listed the examples used throughout this page

#### 1 - Hello world

```cpp
#include <iostream>

using namespace std;

int main(void) {
    cout << "Hello world!" << endl;
    return 0;
}
```

## Namespace

In example 1 we explicitly use the namespace `std`

Without setting the current namespace all element coming from that namespace must be declared as such (`cout` and `endl`)

```cpp
int main(void) {
  std::cout << "It's me, your first program." > std::endl;
  return 0;
}
```

## Preprocessor

## Classes

### Constructors

{% hint style="warning" %}
A constructor cannot be virtual
{% endhint %}

#### Default constructor

#### Copy constructor

#### Move constructor

### Destructors

## Libraries

### iostream

Standard input/output streams

## Compiling with g++

g++ is the C++ pendant of gcc, it recognised types of input files by their extension, optionally the `-x` option can be used to specify a file type

### Basic example, single file

#### Full

Pre-process, compile, assemble, link

```
g++ main.cpp -o main
```

#### Stop after pre-process

The output is a c++ source file that is not supposed to be preprocessed any more

```
g++ -E main.cpp -o main.ii
```

#### Stop after compile

Compile but don't assemble, the output is assembly source code

```
g++ -S main.cpp -o main.s
```

#### Stop after assembly

Compile, and assemble but do not link

```
g++ -c main.cpp -o main.o
```

## Links

* [cplusplus.org](https://cplusplus.com)
