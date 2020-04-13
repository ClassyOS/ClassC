# Classy Specification

## Structure

A classy project can contain multiple numbers of files, each containing different [segments](#Segments).

## Segments

there are four types of segments:

1. The Main Segment

  There can be only one main segment per linked program, and it is used as the program's entery point.

2. Define Segment

  A define segment is a segment just containing [type defenitions](#Type-Defenition). It is only used by the compiler and does not appear in the output binary.

3. Code Segment

  A Code segment contains functions and variables. The variables are local to the segment, but the functions can be called by other segemnts.

4. Data Segment
  A data segment can contain only variables, but unlike code segments, you can refer to the variables in other segments.

### Using Multiple Segments

In order to use a variable, function ot type from another segement, you write the name of the segement and the segment and the name of the function/variable/type, seperated by the scope oporator(::). For example:

``` c
data foo {
    byte bar;
}
...
main requires foo {
    ...
    foo::bar = ...;
}
```

### Defining a Segment

to define a segment, simply write the segment type (main, define, code, data) and put and identefier if needed (on code, data, and define segments). For example:

```c
define types {
    // Type defenitions go here
}

data foo {
    // Variable defenitions go here
}

code bar {
    // Function defenitions go here
}

main {
    // Main code goes gere
}
```

### Linking Segments Togehther

If you want to use a function/variable (__but not type__) from another segment, you need to tell the linker that segment requires getting the address of the other segment. To do that, after the function defenition put the "requires" keyword and the names of the required segments. For example:

```c
data foo {
    ...
}
...
main requires foo {
    ...
}
```

## Type defenition

Type defenitions must be contained within a define segment. Defining a type uses the following syntax:

```c
define types {
    type foo {
        int x;
        byte y;
    }
}
```

you can use any defined type in the subtypes between the brackets, including other defined types:

```c
define types {
    type foo {
        int x;
        byte y;
    }

    type bar {
        foo x;
    }
}
```

If you use a type from a define segment in another file, you can define it in one file and use the include directive:

```c
#include "path/to/file/with/define/segment"
```
## Standard Library

### Output

Output is done through the print function. The print function works by outputting a string that it's been given. Markers in the string signify where to input certain variables. These markers are a single letter surrounded by { }. The variable is then given after the string. See the two examples below.

```c
print("Hello World");
print("{i}", 10);
```

### Input

There are two input functions, read() and scan(). scan() takes input and converts it into a specified type. The below output converts the given input into an int type.

```c
foo = scan(int);
```

read() is the input for a character or string. It works by reading the input until a specified character or character by character without any arguments. The first example below reads a line, the second a character.
```c
foo = read('\n');
bar = read();
```
