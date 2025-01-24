
Why (non-const) global variables are evil

By far the biggest reason non-const global variables are dangerous is because their values can be changed by _any_ function that is called, and there is no easy way for the programmer to know that this will happen. Consider the following program:

```cpp
#include <iostream>

int g_mode; // declare global variable (will be zero-initialized by default)

void doSomething()
{
    g_mode = 2; // set the global g_mode variable to 2
}

int main()
{
    g_mode = 1; // note: this sets the global g_mode variable to 1.  It does not declare a local g_mode variable!

    doSomething();

    // Programmer still expects g_mode to be 1
    // But doSomething changed it to 2!

    if (g_mode == 1)
    {
        std::cout << "No threat detected.\n";
    }
    else
    {
        std::cout << "Launching nuclear missiles...\n";
    }

    return 0;
}
```



In short global variables make the programs state unpredictable. Every function call becomes potentially dangerous.



One of the key reasons to declare local variables as close to where they are used as possible is because doing so minimizes the amount of code you need to look through to understand what the variable does. Global variables are at the opposite end of the spectrum -- because they can be accessed anywhere, you might have to look through the entire program to understand their usage. In small programs, this might not be an issue. In large ones, it will be.




## So what are very good reasons to use non-const global variables?



A good example is a log file, where you can dump error or debug information. It probably makes sense to define this as a global, because you’re likely to only have one such log in a program and it will likely be used everywhere in your program. Another good example would be a random number generator (we show an example of this in lesson [8.15 -- Global random numbers (Random.h)](https://www.learncpp.com/cpp-tutorial/global-random-numbers-random-h/)).


For what it’s worth, the std::cout and std::cin objects are implemented as global variables (inside the _std_ namespace).

First, prefix all non-namespaced global variables with “g” or “g_”, or better yet, put them in a namespace (discussed in lesson [7.2 -- User-defined namespaces and the scope resolution operator](https://www.learncpp.com/cpp-tutorial/user-defined-namespaces-and-the-scope-resolution-operator/)), to reduce the chance of naming collisions.



Second, instead of allowing direct access to the global variable, it’s a better practice to “encapsulate” the variable. Make sure the variable can only be accessed from within the file it’s declared in, e.g. by making the variable static or const, then provide external global “access functions” to work with the variable. These functions can ensure proper usage is maintained (e.g. do input validation, range checking, etc…). Also, if you ever decide to change the underlying implementation (e.g. move from one database to another), you only have to update the access functions instead of every piece of code that uses the global variable directly.


Do this:

```cpp
#include <iostream>

namespace constants
{
    constexpr double gravity { 9.8 };
}

// This function can calculate the instant velocity for any gravity value (more useful)
double instantVelocity(int time, double gravity)
{
    return gravity * time;
}

int main()
{
    std::cout << instantVelocity(5, constants::gravity) << '\n'; // pass our constant to the function as a parameter

    return 0;
}
```


