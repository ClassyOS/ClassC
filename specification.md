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

In order to use a variable or function from another segement, you write the name of the segement and the segment and the name of the function/variable, seperated by the scope oporator(::). For example:

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

to define a segment, simply write the segment type (main, define, code, data) and put and identefier if needed (on code and data segments). For example:

```c
define {
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

If you want to use a function/variable from another segment, you need to tell the linker that segment requires getting the address of the other segment. To do that, after the function defenition put the "requires" keyword and the names of the required segments. For example:

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
