
In lesson [2.5 -- Introduction to local scope](https://web.archive.org/web/20240715201757/https://www.learncpp.com/cpp-tutorial/introduction-to-local-scope/), we introduced `local variables`, which are variables that are defined inside a function (including function parameters).

It turns out that C++ actually doesn’t have a single attribute that defines a variable as being a local variable. Instead, local variables have several different properties that differentiate how these variables behave from other kinds of (non-local) variables. We’ll explore these properties in this and upcoming lessons.

In lesson [2.5 -- Introduction to local scope](https://web.archive.org/web/20240715201757/https://www.learncpp.com/cpp-tutorial/introduction-to-local-scope/), we also introduced the concept of scope. An identifier’s `scope` determines where an identifier can be accessed within the source code. When an identifier can be accessed, we say it is `in scope`. When an identifier can not be accessed, we say it is `out of scope`. Scope is a compile-time property, and trying to use an identifier when it is out of scope will result in a compile error.



Local variables have block scope

Local variables have **block scope**, which means they are _in scope_ from their point of definition to the end of the block they are defined within.

Related content

Please review lesson [7.1 -- Compound statements (blocks)](https://web.archive.org/web/20240715201757/https://www.learncpp.com/cpp-tutorial/compound-statements-blocks/) if you need a refresher on blocks.

```cpp
int main()
{
    int i { 5 }; // i enters scope here
    double d { 4.0 }; // d enters scope here

    return 0;
} // d and i go out of scope here
```


although function parameters are not defined inside the function body, for typical functions they can be considered to be a part of the scope of the function body block


All variable names within a scope must be unique


Local variables have automatic storage duration

A variable’s **storage duration** (usually just called **duration**) determines what rules govern when and how a variable will be created (instantiated) and destroyed. In most cases, a variable’s storage duration directly determines its `lifetime`.


For example, local variables have **automatic storage duration**, which means they are created at the point of definition and destroyed at the end of the block they are defined in. For example:


```cpp
int main()
{
    int i { 5 }; // i created and initialized here
    double d { 4.0 }; // d created and initialized here

    return 0;
} // d and i are destroyed here
```


for this reason local variables are sometimes called automatic variables


## local variables in nested blocks

Local variables can be defined inside nested block. This works identically to local variables in the function body blocks 


```cpp
int main() // outer block
{
    int x { 5 }; // x enters scope and is created here

    { // nested block
        int y { 7 }; // y enters scope and is created here
    } // y goes out of scope and is destroyed here

    // y can not be used here because it is out of scope in this block

    return 0;
} // x goes out of scope and is destroyed here
```

In the above example, variable `y` is defined inside a nested block. Its scope is limited from its point of definition to the end of the nested block, and its lifetime is the same. Because the scope of variable `y` is limited to the inner block in which it is defined, it’s not accessible anywhere in the outer block.

Note that nested blocks are considered part of the scope of the outer block in which they are defined. Consequently, variables defined in the outer block _can_ be seen inside a nested block:

```cpp
#include <iostream>

int main()
{ // outer block

    int x { 5 }; // x enters scope and is created here

    { // nested block
        int y { 7 }; // y enters scope and is created here

        // x and y are both in scope here
        std::cout << x << " + " << y << " = " << x + y << '\n';
    } // y goes out of scope and is destroyed here

    // y can not be used here because it is out of scope in this block

    return 0;
} // x goes out of scope and is destroyed here
```



## local variables have no linkage


identifiers have another property named linkage. An identifiers linkage determine whether a declaration of that same identifier in a different scope refers to the same object or function.

Local variables have no linkage Each declaration of an identifier with no linkage refers to an unique object or function.


Scope and linkage may seem similar. However scope determines where the declaration of a single identifier can be seen and used in code. Linkage determines whether multiple declarations refer to the same object or not.


Variables should be defined in the most limited scope

If a variable is only used within a nested block, it should be defined inside that nested block:


A variable’s scope determines where the variable is accessible within the source code. Duration defines the rules that govern when a variable is created and destroyed. A variable’s lifetime is the actual time between its creation and destruction.

Local variables have block scope, which means they can be accessed from their point of definition to the end of the block they are defined within.

Local variables have automatic duration, which means they are created at the point of definition, and destroyed at the end of the block in which they are defined.