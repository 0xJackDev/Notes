

*The static keyword makes something internally linked* 

Internally linked variables can only be used inside of the cpp file in which it was made in. For example if u define something in a.cpp and try to use it in main.cpp it wont work even if they are compiled together.


In lesson [7.3 -- Local variables](https://web.archive.org/web/20240716020144/https://www.learncpp.com/cpp-tutorial/local-variables/), we said, “An identifier’s linkage determines whether other declarations of that name refer to the same object or not”, and we discussed how local variables have `no linkage`.


Global variable and functions identifiers can have either `internal linkage` or `external linkage`. We’ll cover the internal linkage case in this lesson, and the external linkage case in lesson [7.7 -- External linkage and variable forward declarations](https://web.archive.org/web/20240716020144/https://www.learncpp.com/cpp-tutorial/external-linkage-and-variable-forward-declarations/).


An identifier with **internal linkage** can be seen and used within a single translation unit, but it is not accessible from other translation units (that is, it is not exposed to the linker). This means that if two source files have identically named identifiers with internal linkage, those identifiers will be treated as independent (and do not result in an ODR violation for having duplicate definitions).


Global variables with internal linkage

Global variables with internal linkage are sometimes called **internal variables**.

To make a non-constant global variable internal, we use the `static` keyword.

```cpp
#include <iostream>

static int g_x{}; // non-constant globals have external linkage by default, but can be given internal linkage via the static keyword

const int g_y{ 1 }; // const globals have internal linkage by default
constexpr int g_z{ 2 }; // constexpr globals have internal linkage by default

int main()
{
    std::cout << g_x << ' ' << g_y << ' ' << g_z << '\n';
    return 0;
}
```

Const and constexpr global variables have internal linkage by default (and thus don’t need the `static` keyword -- if it is used, it will be ignored).

Here’s an example of multiple files using internal variables:

a.cpp:

```cpp
[[maybe_unused]] constexpr int g_x { 2 }; // this internal g_x is only accessible within a.cpp
```

main.cpp:

```cpp
#include <iostream>

static int g_x { 3 }; // this separate internal g_x is only accessible within main.cpp

int main()
{
    std::cout << g_x << '\n'; // uses main.cpp's g_x, prints 3

    return 0;
}
```

This program prints:

3

Because `g_x` is internal to each file, `main.cpp` has no idea that `a.cpp` also has a variable named `g_x` (and vice versa).



The one-definition rule and internal linkage

In lesson [2.7 -- Forward declarations and definitions](https://web.archive.org/web/20240716020144/https://www.learncpp.com/cpp-tutorial/forward-declarations/), we noted that the one-definition rule says that an object or function can’t have more than one definition, either within a file or a program.

However, it’s worth noting that internal objects (and functions) that are defined in different files are considered to be independent entities (even if their names and types are identical), so there is no violation of the one-definition rule. Each internal object only has one definition.


Learn CPP 7.7:


In the prior lesson ([7.6 -- Internal linkage](https://web.archive.org/web/20240716020514/https://www.learncpp.com/cpp-tutorial/internal-linkage/)), we discussed how `internal linkage` limits the use of an identifier to a single file. In this lesson, we’ll explore the concept of `external linkage`.

An identifier with **external linkage** can be seen and used both from the file in which it is defined, and from other code files (via a forward declaration). In this sense, identifiers with external linkage are truly “global” in that they can be used anywhere in your program!


Functions have external linkage by default

In lesson [2.8 -- Programs with multiple code files](https://web.archive.org/web/20240716020514/https://www.learncpp.com/cpp-tutorial/programs-with-multiple-code-files/), you learned that you can call a function defined in one file from another file. This is because functions have external linkage by default.

In order to call a function defined in another file, you must place a `forward declaration` for the function in any other files wishing to use the function. The forward declaration tells the compiler about the existence of the function, and the linker connects the function calls to the actual function definition.

Here’s an example:

a.cpp:

```cpp
#include <iostream>

void sayHi() // this function has external linkage, and can be seen by other files
{
    std::cout << "Hi!\n";
}
```

main.cpp:

```cpp
void sayHi(); // forward declaration for function sayHi, makes sayHi accessible in this file

int main()
{
    sayHi(); // call to function defined in another file, linker will connect this call to the function definition

    return 0;
}
```

The above program prints:

Hi!

In the above example, the forward declaration of function `sayHi()` in `main.cpp` allows `main.cpp` to access the `sayHi()` function defined in `a.cpp`. The forward declaration satisfies the compiler, and the linker is able to link the function call to the function definition.

If function `sayHi()` had internal linkage instead, the linker would not be able to connect the function call to the function definition, and a linker error would result.



Global variables with external linkage

Global variables with external linkage are sometimes called **external variables**. To make a global variable external (and thus accessible by other files), we can use the `extern` keyword to do so:

```cpp
int g_x { 2 }; // non-constant globals are external by default

extern const int g_y { 3 }; // const globals can be defined as extern, making them external
extern constexpr int g_z { 3 }; // constexpr globals can be defined as extern, making them external (but this is pretty useless, see the warning in the next section)

int main()
{
    return 0;
}
```

Non-const global variables are external by default (if used, the `extern` keyword will be ignored).



Variable forward declarations via the extern keyword

To actually use an external global variable that has been defined in another file, you also must place a `forward declaration` for the global variable in any other files wishing to use the variable. For variables, creating a forward declaration is also done via the `extern` keyword (with no initialization value).

Here is an example of using a variable forward declaration:

a.cpp:

```cpp
// global variable definitions
int g_x { 2 }; // non-constant globals have external linkage by default
extern const int g_y { 3 }; // this extern gives g_y external linkage
```

main.cpp:

```cpp
#include <iostream>

extern int g_x; // this extern is a forward declaration of a variable named g_x that is defined somewhere else
extern const int g_y; // this extern is a forward declaration of a const variable named g_y that is defined somewhere else

int main()
{
    std::cout << g_x << ' ' << g_y << '\n'; // prints 2 3

    return 0;
}
```

In the above example, `a.cpp` and `main.cpp` both reference the same global variable named `g_x`. So even though `g_x` is defined and initialized in `a.cpp`, we are able to use its value in `main.cpp` via the forward declaration of `g_x`.

Note that the `extern` keyword has different meanings in different contexts. In some contexts, `extern` means “give this variable external linkage”. In other contexts, `extern` means “this is a forward declaration for an external variable that is defined somewhere else”. Yes, this is confusing, so we summarize all of these usages in lesson [7.11 -- Scope, duration, and linkage summary](https://web.archive.org/web/20240716020514/https://www.learncpp.com/cpp-tutorial/scope-duration-and-linkage-summary/).


Scope determines where a variable is accessible. Duration determines when a variable is created and destroyed. Linkage determines whether the variable can be exported to another file or not.

Global variables have global scope (a.k.a. file scope), which means they can be accessed from the point of declaration to the end of the file in which they are declared.

Global variables have static duration, which means they are created when the program is started, and destroyed when it ends.

Global variables can have either internal or external linkage, via the static and extern keywords respectively.