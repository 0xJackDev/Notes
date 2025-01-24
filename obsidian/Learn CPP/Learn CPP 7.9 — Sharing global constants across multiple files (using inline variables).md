

In some applications, certain symbolic constants may need to be used throughout your code (not just in one location). These can include physics or mathematical constants that don’t change (e.g. pi or Avogadro’s number), or application-specific “tuning” values (e.g. friction or gravity coefficients). Instead of redefining these constants in every file that needs them (a violation of the “Don’t Repeat Yourself” rule), it’s better to declare them once in a central location and use them wherever needed. That way, if you ever need to change them, you only need to change them in one place, and those changes can be propagated out.



Prior to C++ 17 the easiest way to do this was:
1. Create a header file to hold all the constants
2. Inside this header file define a namespace
3. Add all your constants inside the namespace (make sure they are constexpr not just const)
4. #include the header file whenever you need it 
5. Make sure you have header guards too! e.g #pragma once
\


When this header gets #included into a .cpp file, each of these variables defined in the header will be copied into that code file at the point of inclusion. Because these variables live outside of a function, they’re treated as global variables within the file they are included into, which is why you can use them anywhere in that file.



## global constants as external variables

The above method has a few problems. For example everytime the header file gets included into a different code file each of these variables is copied into the code file. Therefore if the header is included in 20 code files these variables are duplicated 20 times. Header guards dont stop this they only prevent a header from being included more then once into a single included file not from being included multiple times in different code files.



1. Changing a single constant value would require recompiling every file that includes the constants header, which can lead to lengthy rebuild times for larger projects.
2. If the constants are large in size and can’t be optimized away, this can use a lot of memory.

One way to avoid these problems is by turning these constants into external variables, since we can then have a single variable (initialized once) that is shared across all files. In this method, we’ll define the constants in a .cpp file (to ensure the definitions only exist in one place), and put forward declarations in the header (which will be included by other files).



constants.cpp:

```cpp
#include "constants.h"

namespace constants
{
    // actual global variables
    extern constexpr double pi { 3.14159 };
    extern constexpr double avogadro { 6.0221413e23 };
    extern constexpr double myGravity { 9.2 }; // m/s^2 -- gravity is light on this planet
}
```

Copy

constants.h:

```cpp
#ifndef CONSTANTS_H
#define CONSTANTS_H

namespace constants
{
    // since the actual variables are inside a namespace, the forward declarations need to be inside a namespace as well
    // we can't forward declare variables as constexpr, but we can forward declare them as (runtime) const
    extern const double pi;
    extern const double avogadro;
    extern const double myGravity;
}

#endif
```

Copy

Use in the code file stays the same:

main.cpp:

```cpp
#include "constants.h" // include all the forward declarations

#include <iostream>

int main()
{
    std::cout << "Enter a radius: ";
    double radius{};
    std::cin >> radius;

    std::cout << "The circumference is: " << 2 * radius * constants::pi << '\n';

    return 0;
}
```



feel free that instead of #ifdef to use #pragma once


However, there are a couple of downsides to this method. First, these constants are now considered compile-time constants only within the file they are actually defined in (`constants.cpp`). In other files, the compiler will only see the forward declaration, which doesn’t define a constexpr value (and must be resolved by the linker). This means in other files, these are treated as runtime constant values, not compile-time constants. Thus outside of `constants.cpp`, these variables can’t be used anywhere that requires a compile-time constant. Second, because compile-time constants can typically be optimized more than runtime constants, the compiler may not be able to optimize these as much.



Best practice

If you need global constants and your compiler is C++17 capable, prefer defining inline constexpr global variables in a header file.


A reminder

Use `std::string_view` for `constexpr` strings. We cover this in lesson [5.10 -- Introduction to std::string_view](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring_view/).