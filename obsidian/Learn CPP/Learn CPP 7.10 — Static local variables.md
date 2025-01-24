The term `static` is one of the most confusing terms in the C++ language, in large part because `static` has different meanings in different contexts.

In prior lessons, we covered that global variables have `static duration`, which means they are created when the program starts and destroyed when the program ends.

We also discussed how the `static` keyword gives a global identifier `internal linkage`, which means the identifier can only be used in the file in which it is defined.

In this lesson, we’ll explore the use of the `static` keyword when applied to a local variable.



In lesson [2.5 -- Introduction to local scope](https://www.learncpp.com/cpp-tutorial/introduction-to-local-scope/), you learned that local variables have `automatic duration` by default, which means they are created at the point of definition, and destroyed when the block is exited.

Using the `static` keyword on a local variable changes its duration from `automatic duration` to `static duration`. This means the variable is now created at the start of the program, and destroyed at the end of the program (just like a global variable). As a result, the static variable will retain its value even after it goes out of scope!


The easiest way to show the difference between `automatic duration` and `static duration` local variables is by example.

Automatic duration (default):

```cpp
#include <iostream>

void incrementAndPrint()
{
    int value{ 1 }; // automatic duration by default
    ++value;
    std::cout << value << '\n';
} // value is destroyed here

int main()
{
    incrementAndPrint();
    incrementAndPrint();
    incrementAndPrint();

    return 0;
}
```

Copy

Each time incrementAndPrint() is called, a variable named value is created and assigned the value of 1. incrementAndPrint() increments value to 2, and then prints the value of 2. When incrementAndPrint() is finished running, the variable goes out of scope and is destroyed. Consequently, this program outputs:

2
2
2

Now consider a version of this program that uses a static local variable. The only difference between this and the above program is that we’ve changed the local variable from `automatic duration` to `static duration` by using the `static` keyword.

Static duration (using static keyword):

```cpp
#include <iostream>

void incrementAndPrint()
{
    static int s_value{ 1 }; // static duration via static keyword.  This initializer is only executed once.
    ++s_value;
    std::cout << s_value << '\n';
} // s_value is not destroyed here, but becomes inaccessible because it goes out of scope

int main()
{
    incrementAndPrint();
    incrementAndPrint();
    incrementAndPrint();

    return 0;
}
```

Copy

In this program, because `s_value` has been declared as `static`, it is created at the program start.

Static local variables that are zero initialized or have a constexpr initializer can be initialized at program start.

Static local variables that have no initializer or a non-constexpr initializer are zero-initialized at program start. Static local variables with a non-constexpr initializer are reinitialized the first time the variable definition is encountered. The definition is skipped on subsequent calls, so no futher reinitialization happens. Because they have static duration, static local variables that are not explicitly initialized will be zero-initialized by default.

Because `s_value` has constexpr initializer `1`, `s_value` will be initialized at program start.

When `s_value` goes out of scope at the end of the function, it is not destroyed. Each time the function incrementAndPrint() is called, the value of `s_value` remains at whatever we left it at previously. Consequently, this program outputs:

2
3
4




Just like we use the g_ prefix for global variables we use the s_ prefix for static duration local variables




ID generation

One of the most common uses for static duration local variables is for unique ID generators. Imagine a program where you have many similar objects (e.g. a game where you’re being attacked by many zombies, or a simulation where you’re displaying many triangles). If you notice a defect, it can be near impossible to distinguish which object is having problems. However, if each object is given a unique identifier upon creation, then it can be easier to differentiate the objects for further debugging.

Generating a unique ID number is very easy to do with a static duration local variable:

```cpp
int generateID()
{
    static int s_itemID{ 0 };
    return s_itemID++; // makes copy of s_itemID, increments the real s_itemID, then returns the value in the copy
}
```

Copy

The first time this function is called, it returns 0. The second time, it returns 1. Each time it is called, it returns a number one higher than the previous time it was called. You can assign these numbers as unique IDs for your objects. Because `s_itemID` is a local variable, it can not be “tampered with” by other functions.



Static local constants

Static local variables can be made const (or constexpr). One good use for a const static local variable is when you have a function that needs to use a const value, but creating or initializing the object is expensive (e.g. you need to read the value from a database). If you used a normal local variable, the variable would be created and initialized every time the function was executed. With a const/constexpr static local variable, you can create and initialize the expensive object once, and then reuse it whenever the function is called.



When applied to a global variable, the static keyword defines the global variable as having internal linkage, meaning the variable cannot be exported to other files.

When applied to a local variable, the static keyword defines the local variable as having static duration, meaning the variable will only be created once, and will not be destroyed until the end of the program.



