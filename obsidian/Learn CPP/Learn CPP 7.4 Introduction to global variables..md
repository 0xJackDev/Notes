

Local variables are variables defined inside a function body. Local variables have a block scope (and are only visible within the block they are declared in) and have automatic duration.


In C++ variables declared outside of a function block are called global variables




## Declaring global variables.


By convention, global variables are declared at the top of a file, below the includes in the global namespace an global variable being defined


```cpp
#include <iostream>

// Variables declared outside of a function are global variables
int g_x {}; // global variable g_x

void doSomething()
{
    // global variables can be seen and used everywhere in the file
    g_x = 3;
    std::cout << g_x << '\n';
}

int main()
{
    doSomething();
    std::cout << g_x << '\n';

    // global variables can be seen and used everywhere in the file
    g_x = 5;
    std::cout << g_x << '\n';

    return 0;
}
// g_x goes out of scope here
```

The above example prints:

3
3
5




The scope of global variables

Identifiers declared in the global namespace have **global namespace scope** (commonly called **global scope**, and sometimes informally called **file scope**), which means they are visible from the point of declaration until the end of the _file_ in which they are declared.

Once declared, a global variable can be used anywhere in the file from that point onward! In the above example, global variable `g_x` is used in both functions `doSomething()` and `main()`.

Global variables can also be defined inside a user-defined namespace. Here is the same example as above, but `g_x` has been moved from the global scope into user-defined namespace `Foo`:

```cpp
#include <iostream>

namespace Foo // Foo is defined in the global scope
{
    int g_x {}; // g_x is now inside the Foo namespace, but is still a global variable
}

void doSomething()
{
    // global variables can be seen and used everywhere in the file
    Foo::g_x = 3;
    std::cout << Foo::g_x << '\n';
}

int main()
{
    doSomething();
    std::cout << Foo::g_x << '\n';

    // global variables can be seen and used everywhere in the file
    Foo::g_x = 5;
    std::cout << Foo::g_x << '\n';

    return 0;
}
```

Although the identifier `g_x` is now limited to the scope of `namespace Foo`, that name is still globally accessible (via `Foo::g_x`), and `g_x` is still a global variable.

Key insight

Variables declared inside a namespace are also global variables.

Best practice

Prefer defining global variables inside a namespace rather than in the global namespace.




Global variables have static duration

Global variables are created when the program starts (before `main()` begins execution), and destroyed when it ends. This is called **static duration**. Variables with _static duration_ are sometimes called **static variables**.


Naming global variables

By convention, some developers prefix global variable identifiers with “g” or “g_” to indicate that they are global. This prefix serves several purposes:



Global variable initialization

Unlike local variables, which are uninitialized by default, variables with static duration are zero-initialized by default.

Non-constant global variables can be optionally initialized:

```cpp
int g_x;       // no explicit initializer (zero-initialized by default)
int g_y {};    // value initialized (resulting in zero-initialization)
int g_z { 1 }; // list initialized with specific value
```



Constant global variables

Just like local variables, global variables can be constant. As with all constants, constant global variables must be initialized.

```cpp
#include <iostream>

const int g_x;     // error: constant variables must be initialized
constexpr int g_w; // error: constexpr variables must be initialized

const int g_y { 1 };     // const global variable g_y, initialized with a value
constexpr int g_z { 2 }; // constexpr global variable g_z, initialized with a value

void doSomething()
{
    // global variables can be seen and used everywhere in the file
    std::cout << g_y << '\n';
    std::cout << g_z << '\n';
}

int main()
{
    doSomething();

    // global variables can be seen and used everywhere in the file
    std::cout << g_y << '\n';
    std::cout << g_z << '\n';

    return 0;
}
// g_y and g_z goes out of scope here
```






A word of caution about (non-constant) global variables

New programmers are often tempted to use lots of global variables, because they can be used without having to explicitly pass them to every function that needs them. However, use of non-constant global variables should generally be avoided altogether! We’ll discuss why in upcoming lesson [7.8 -- Why (non-const) global variables are evil](https://web.archive.org/web/20240715201801/https://www.learncpp.com/cpp-tutorial/why-non-const-global-variables-are-evil/).



