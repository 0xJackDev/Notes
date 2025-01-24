

Type aliases

In C++, **using** is a keyword that creates an alias for an existing data type. To create such a type alias, we use the `using` keyword, followed by a name for the type alias, followed by an equals sign and an existing data type. For example:

```cpp
using Distance = double; // define Distance as an alias for type double
```

Copy

Once defined, a type alias can be used anywhere a type is needed. For example, we can create a variable with the type alias name as the type:

```cpp
Distance milesToDestination{ 3.4 }; // defines a variable of type double
```

Copy

When the compiler encounters a type alias name, it will substitute in the aliased type. For example:

```cpp
#include <iostream>

int main()
{
    using Distance = double; // define Distance as an alias for type double

    Distance milesToDestination{ 3.4 }; // defines a variable of type double

    std::cout << milesToDestination << '\n'; // prints a double value

    return 0;
}
```

Copy

This prints:




Best practice
Name your type aliases starting with a capital letter and do not use a suffix (unless you have a specific reason to do otherwise).



Type aliases are not distinct types

An alias does not actually define a new, distinct type (one that is considered separate from other types) -- it just introduces a new identifier for an existing type. A type alias is completely interchangeable with the aliased type.



The scope of a type alias

Because scope is a property of an identifier, type alias identifiers follow the same scoping rules as variable identifiers: a type alias defined inside a block has block scope and is usable only within that block, whereas a type alias defined in the global namespace has global scope and is usable to the end of the file. In the above example, `Miles` and `Speed` are only usable in the `main()` function.



Typedefs

A **typedef** (which is short for “type definition”) is an older way of creating an alias for a type. To create a typedef alias, we use the `typedef` keyword:

Prefer the using keyword over typedef. 



Using type aliases for platform independent coding

One of the primary uses for type aliases is to hide platform specific details. On some platforms, an `int` is 2 bytes, and on others, it is 4 bytes. Thus, using `int` to store more than 2 bytes of information can be potentially dangerous when writing platform independent code.

Because `char`, `short`, `int`, and `long` give no indication of their size, it is fairly common for cross-platform programs to use type aliases to define aliases that include the type’s size in bits. For example, `int8_t` would be an 8-bit signed integer, `int16_t` a 16-bit signed integer, and `int32_t` a 32-bit signed integer. Using type aliases in this manner helps prevent mistakes and makes it more clear about what kind of assumptions have been made about the size of the variable.

In order to make sure each aliased type resolves to a type of the right size, type aliases of this kind are typically used in conjunction with preprocessor directives:

```cpp
#ifdef INT_2_BYTES
using int8_t = char;
using int16_t = int;
using int32_t = long;
#else
using int8_t = char;
using int16_t = short;
using int32_t = int;
#endif
```



Using type aliases to make complex types easier to read

Although we have only dealt with simple data types so far, in advanced C++, types can be complicated and lengthy to manually enter on your keyboard. For example, you might see a function and variable defined like this:

```cpp
#include <string> // for std::string
#include <vector> // for std::vector
#include <utility> // for std::pair

bool hasDuplicates(std::vector<std::pair<std::string, int>> pairlist)
{
    // some code here
    return false;
}

int main()
{
     std::vector<std::pair<std::string, int>> pairlist;

     return 0;
}
```

Copy

Typing `std::vector<std::pair<std::string, int>>` everywhere you need to use that type is cumbersome, and it is easy to make a typing mistake. It’s much easier to use a type alias:

```cpp
#include <string> // for std::string
#include <vector> // for std::vector
#include <utility> // for std::pair

using VectPairSI = std::vector<std::pair<std::string, int>>; // make VectPairSI an alias for this crazy type

bool hasDuplicates(VectPairSI pairlist) // use VectPairSI in a function parameter
{
    // some code here
    return false;
}

int main()
{
     VectPairSI pairlist; // instantiate a VectPairSI variable

     return 0;
}
```

Copy

Much better! Now we only have to type `VectPairSI` instead of `std::vector<std::pair<std::string, int>>`.

Don’t worry if you don’t know what `std::vector`, `std::pair`, or all these crazy angle brackets are yet. The only thing you really need to understand here is that type aliases allow you to take complex types and give them a simpler name, which makes your code easier to read and saves typing.

This is probably the best use for type aliases.



