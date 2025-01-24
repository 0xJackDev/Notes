Defining your own namespaces

C++ allows us to define our own namespaces via the `namespace` keyword. Namespaces that you create in your own programs are casually called **user-defined namespaces** (though it would be more accurate to call them **program-defined namespaces**).


The syntax for a namespace is as follows:

namespace NamespaceIdentifier
{
    // content of namespace here
}


Historically, namespace names have not been capitalized, and many style guides still recommend this convention.


A namespace must be defined either in the global scope, or inside another namespace. Much like the content of a function, the content of a namespace is conventionally indented one level. You may occasionally see an optional semicolon placed after the closing brace of a namespace.

Here is an example of the files in the prior example rewritten using namespaces:

foo.cpp:

```cpp
namespace Foo // define a namespace named Foo
{
    // This doSomething() belongs to namespace Foo
    int doSomething(int x, int y)
    {
        return x + y;
    }
}
```

Copy

goo.cpp:

```cpp
namespace Goo // define a namespace named Goo
{
    // This doSomething() belongs to namespace Goo
    int doSomething(int x, int y)
    {
        return x - y;
    }
}
```

Copy

Now `doSomething()` inside of `foo.cpp` is inside the `Foo` namespace, and the `doSomething()` inside of `goo.cpp` is inside the `Goo` namespace. Let’s see what happens when we recompile our program.

main.cpp:

```cpp
int doSomething(int x, int y); // forward declaration for doSomething

int main()
{
    std::cout << doSomething(4, 3) << '\n'; // which doSomething will we get?
    return 0;
}
```

Copy

The answer is that we now get another error!

ConsoleApplication1.obj : error LNK2019: unresolved external symbol "int __cdecl doSomething(int,int)" (?doSomething@@YAHHH@Z) referenced in function _main

In this case, the compiler was satisfied (by our forward declaration), but the linker could not find a definition for `doSomething` in the global namespace. This is because both of our versions of `doSomething` are no longer in the global namespace! They are now in the scope of their respective namespaces!

There are two different ways to tell the compiler which version of `doSomething()` to use, via the `scope resolution operator`, or via `using statements` (which we’ll discuss in a later lesson in this chapter).

For the subsequent examples, we’ll collapse our examples down to a one-file solution for ease of reading.

Accessing a namespace with the scope resolution operator (::)

The best way to tell the compiler to look in a particular namespace for an identifier is to use the **scope resolution operator** (::). The scope resolution operator tells the compiler that the identifier specified by the right-hand operand should be looked for in the scope of the left-hand operand.

Here is an example of using the scope resolution operator to tell the compiler that we explicitly want to use the version of `doSomething()` that lives in the `Foo` namespace:

```cpp
#include <iostream>

namespace Foo // define a namespace named Foo
{
    // This doSomething() belongs to namespace Foo
    int doSomething(int x, int y)
    {
        return x + y;
    }
}

namespace Goo // define a namespace named Goo
{
    // This doSomething() belongs to namespace Goo
    int doSomething(int x, int y)
    {
        return x - y;
    }
}

int main()
{
    std::cout << Foo::doSomething(4, 3) << '\n'; // use the doSomething() that exists in namespace Foo
    return 0;
}
```

Copy

This produces the expected result:

7

If we wanted to use the version of `doSomething()` that lives in `Goo` instead:

```cpp
#include <iostream>

namespace Foo // define a namespace named Foo
{
    // This doSomething() belongs to namespace Foo
    int doSomething(int x, int y)
    {
        return x + y;
    }
}

namespace Goo // define a namespace named Goo
{
    // This doSomething() belongs to namespace Goo
    int doSomething(int x, int y)
    {
        return x - y;
    }
}

int main()
{
    std::cout << Goo::doSomething(4, 3) << '\n'; // use the doSomething() that exists in namespace Goo
    return 0;
}
```

Copy

This produces the result:

1

The scope resolution operator is great because it allows us to _explicitly_ pick which namespace we want to look in, so there’s no potential ambiguity. We can even do the following:



Forward declaration of content in namespaces

In lesson [2.11 -- Header files](https://www.learncpp.com/cpp-tutorial/header-files/), we discussed how we can use header files to propagate forward declarations. For identifiers inside a namespace, those forward declarations also need to be inside the same namespace:

add.h

```cpp
#ifndef ADD_H
#define ADD_H

namespace BasicMath
{
    // function add() is part of namespace BasicMath
    int add(int x, int y);
}

#endif
```

Copy

add.cpp

```cpp
#include "add.h"

namespace BasicMath
{
    // define the function add() inside namespace BasicMath
    int add(int x, int y)
    {
        return x + y;
    }
}
```

Copy

main.cpp

```cpp
#include "add.h" // for BasicMath::add()

#include <iostream>

int main()
{
    std::cout << BasicMath::add(4, 3) << '\n';

    return 0;
}
```

Copy

If the forward declaration for `add()` wasn’t placed inside namespace `BasicMath`, then `add()` would be declared in the global namespace instead, and the compiler would complain that it hadn’t seen a declaration for the call to `BasicMath::add(4, 3)`. If the definition of function `add()` wasn’t inside namespace `BasicMath`, the linker would complain that it couldn’t find a matching definition for the call to `BasicMath::add(4, 3)`.



Multiple namespace blocks are allowed

It’s legal to declare namespace blocks in multiple locations (either across multiple files, or multiple places within the same file). All declarations within the namespace are considered part of the namespace.

circle.h:

```cpp
#ifndef CIRCLE_H
#define CIRCLE_H

namespace BasicMath
{
    constexpr double pi{ 3.14 };
}

#endif
```

Copy

growth.h:

```cpp
#ifndef GROWTH_H
#define GROWTH_H

namespace BasicMath
{
    // the constant e is also part of namespace BasicMath
    constexpr double e{ 2.7 };
}

#endif
```

Copy

main.cpp:

```cpp
#include "circle.h" // for BasicMath::pi
#include "growth.h" // for BasicMath::e

#include <iostream>

int main()
{
    std::cout << BasicMath::pi << '\n';
    std::cout << BasicMath::e << '\n';

    return 0;
}
```

Copy

This works exactly as you would expect:

3.14
2.7

The standard library makes extensive use of this feature, as each standard library header file contains its declarations inside a `namespace std` block contained within that header file. Otherwise the entire standard library would have to be defined in a single header file!

Note that this capability also means you could add your own functionality to the `std` namespace. Doing so causes undefined behavior most of the time, because the `std` namespace has a special rule prohibiting extension from user code.


Warning

Do not add custom functionality to the std namespace.

Nested namespaces

Namespaces can be nested inside other namespaces. For example:

```cpp
#include <iostream>

namespace Foo
{
    namespace Goo // Goo is a namespace inside the Foo namespace
    {
        int add(int x, int y)
        {
            return x + y;
        }
    }
}

int main()
{
    std::cout << Foo::Goo::add(1, 2) << '\n';
    return 0;
}
```

Copy

Note that because namespace `Goo` is inside of namespace `Foo`, we access `add` as `Foo::Goo::add`.

Since C++17, nested namespaces can also be declared this way:

```cpp
#include <iostream>

namespace Foo::Goo // Goo is a namespace inside the Foo namespace (C++17 style)
{
    int add(int x, int y)
    {
        return x + y;
    }
}

int main()
{
    std::cout << Foo::Goo::add(1, 2) << '\n';
    return 0;
}
```

Copy

This is equivalent to the prior example.

If you later need to add declarations to the `Foo` namespace (only), you can define a separate `Foo` namespace to do so:

```cpp
#include <iostream>

namespace Foo::Goo // Goo is a namespace inside the Foo namespace (C++17 style)
{
    int add(int x, int y)
    {
        return x + y;
    }
}

namespace Foo
{
     void someFcn() {} // This function is in Foo only
}

int main()
{
    std::cout << Foo::Goo::add(1, 2) << '\n';
    return 0;
}
```

Copy

Whether you keep the separate `Foo::Goo` definition or nest `Goo` inside `Foo` is a stylistic choice.



How to use namespaces

It’s worth noting that namespaces in C++ were not originally designed as a way to implement an information hierarchy -- they were designed primarily as a mechanism for preventing naming collisions. As evidence of this, note that the entirety of the standard library lives under the single top-level namespace `std`. Newer standard library features that introduce lots of names have started using nested namespaces (e.g. `std::ranges`) to avoid naming collisions within the `std` namespace.

- Small applications developed for your own use typically do not need to be placed in namespaces. However, for larger personal projects that include lots of third party libraries, namespacing your code can help prevent naming collisions with libraries that aren’t properly namespaced.

Author’s note

The examples in these tutorials will typically not be namespaced unless we are illustrating something specific about namespaces, to help keep the examples concise.

- Any code that will be distributed to others should definitely be namespaced to prevent conflicts with the code it is integrated into. Often a single top-level namespace will suffice (e.g. `Foologger`). As an additional advantage, placing library code inside a namespace also allows the user to see the contents of your library by using their editor’s auto-complete and suggestion feature (e.g. if you type `Foologger`, autocomplete will show you all of the names inside `Foologger`).
- In multi-team organizations, two-level or even three-level namespaces are often used to prevent naming conflicts between code generated by different teams. These often take the form of one of the following:

1. Project or library :: module (e.g. `Foologger::Lang`)
2. Company or org :: project or library (e.g. `Foosoft::Foologger`)
3. Company or org :: project or library :: module (e.g. `Foosoft::Foologger::Lang`)

Use of module-level namespaces can help separate code that might be reusable later from application-specific code that will not be reusable. For example, physics and math functions could go into one namespace (e.g. `Math::`). Language and localization functions in another (e.g. `Lang::`). However, directory structures can also be used for this (with app-specific code in the project directory tree, and reusable code in a separate shared directory tree).

In general, you should avoid deeply nested namespaces (more than 3 levels).