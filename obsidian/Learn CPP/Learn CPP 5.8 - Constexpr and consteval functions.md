
we introduced the constexpr keyword which we used to create compile-time constants. 


One challenge with constant expressions is that function call to a normal function isnt allowed in them. 


Consider the following program:

```cpp
#include <iostream>

int main()
{
    constexpr double radius { 3.0 };
    constexpr double pi { 3.14159265359 };
    constexpr double circumference { 2.0 * radius * pi };

    std::cout << "Our circle has circumference " << circumference << "\n";

    return 0;
}
```

Copy

This produces the result:

Our circle has circumference 18.8496

Having a complex initializer for `circumference` isn’t great (and requires us to instantiate two supporting variables, `radius` and `pi`). So let’s make it a function instead:

```cpp
#include <iostream>

double calcCircumference(double radius)
{
    constexpr double pi { 3.14159265359 };
    return 2.0 * pi * radius;
}

int main()
{
    constexpr double circumference { calcCircumference(3.0) }; // compile error

    std::cout << "Our circle has circumference " << circumference << "\n";

    return 0;
}
```

Copy

This code is much cleaner. It also doesn’t compile. Constexpr variable `circumference` requires that its initializer is a constant expression, and the call `calcCircumference()` isn’t a constant expression.

In this particular case, we could make `circumference` non-constexpr, and the program would compile. While we’d lose the benefits of constant expressions, at least the program would run.

However, there are other cases in C++ (which we’ll introduce in the future) where we do not have alternate options available, and only a constant expression will do. In those cases, we’d really like to be able to use functions, but calls to normal functions just won’t work. So what are we to do?.



## Constexpr functions can be used in constant expressions

A **constexpr function** is a function that is allowed to be called in a constant expression.

To make a function a constexpr function, we simply use the `constexpr` keyword in front of the function’s return type.

Key insight

The `constexpr` keyword is used to signal to the compiler and other developers that a function can be used in a constant expression.

Here’s the same example as above, but using a constexpr function:

```cpp
#include <iostream>

constexpr double calcCircumference(double radius) // now a constexpr function
{
    constexpr double pi { 3.14159265359 };
    return 2.0 * pi * radius;
}

int main()
{
    constexpr double circumference { calcCircumference(3.0) }; // now compiles

    std::cout << "Our circle has circumference " << circumference << "\n";

    return 0;
}
```

Copy

Because `calcCircumference()` is now a constexpr function, it can be used in a constant expression, such as the initializer of `circumference`.




## Constexpr functions can be evaluated at compile time 

A constant expression is required to evaluate at compile time. If a required const expression contain a constexpr function call then the constexpr function call MUST also evaluate at compile time.

In our example above, variable `circumference` is constexpr and thus requires a constant expression initializer. Since `calcCircumference()` is part of this required constant expression, `calcCircumference()` must be evaluated at compile-time.

So in our example, the call to `calcCircumference(3.0)` is replaced with the result of the function call, which is `18.8496`. In other words, the compiler will compile this:


To evaluate at compile-time, two other things must also be true:

- The call to the constexpr function must have arguments that are known at compile time (e.g. are constant expressions).
- All statements and expressions within the constexpr function must be evaluatable at compile-time.

When a constexpr (or consteval) function is being evaluated at compile-time, any other functions it calls are required to be evaluated at compile-time (otherwise the initial function would not be able to return a result at compile-time).


Constexpr function calls in non-required constant expressions

You might expect that a constexpr function would evaluate at compile-time whenever possible, but unfortunately this is not the case.

In lesson [5.4 -- Constant expressions and compile-time optimization](https://www.learncpp.com/cpp-tutorial/constant-expressions-and-compile-time-optimization/), we noted that in contexts that do not _require_ a constant expression, the compiler may choose whether to evaluate a constant expression at either compile-time or at runtime. Accordingly, any constexpr function call that is part of a non-required constant expression may be evaluated at either compile-time or runtime.

For example:

```cpp
#include <iostream>

constexpr int getValue(int x)
{
    return x;
}

int main()
{
    int x { getValue(5) }; // may evaluate at runtime or compile-time

    return 0;
}
```

Copy

In the above example, because `getValue()` is constexpr, the call `getValue(5)` is a constant expression. However, because variable `x` is not constexpr, it does not require a constant expression initializer. So even though we’ve provided a constant expression initializer, the compiler is free to choose whether `getValue(5)` evaluates at runtime or compile-time.


Constexpr functions are implicitly inline

*Key insight

Put another way, we can categorize the likelihood that a function will actually be evaluated at compile-time as follows:

Always (required by the standard):

- Constexpr function is called where constant expression is required.
- Constexpr function is called from other function being evaluated at compile-time.

Probably (there’s little reason not to):

- Constexpr function is called where constant expression isn’t required, all arguments are constant expressions.

Possibly (if optimized under the as-if rule):

- Constexpr function is called where constant expression isn’t required, some arguments are not constant expressions but their values are known at compile-time.
- Non-constexpr function capable of being evaluated at compile-time, all arguments are constant expressions.

Never (not possible):

- Constexpr function is called where constant expression isn’t required, some arguments have values that are not known at compile-time.*




## Consteval C++20

C++20 introduces the keyword **consteval**, which is used to indicate that a function _must_ evaluate at compile-time, otherwise a compile error will result. Such functions are called **immediate functions**.

```cpp
#include <iostream>

consteval int greater(int x, int y) // function is now consteval
{
    return (x > y ? x : y);
}

int main()
{
    constexpr int g { greater(5, 6) };              // ok: will evaluate at compile-time
    std::cout << g << '\n';

    std::cout << greater(5, 6) << " is greater!\n"; // ok: will evaluate at compile-time

    int x{ 5 }; // not constexpr
    std::cout << greater(x, 6) << " is greater!\n"; // error: consteval functions must evaluate at compile-time

    return 0;
}
```

Copy

In the above example, the first two calls to `greater()` will evaluate at compile-time. The call to `greater(x, 6)` cannot be evaluated at compile-time, so a compile error will result.

Best practice

Use `consteval` if you have a function that must evaluate at compile-time for some reason (e.g. because it does something that can only be done at compile time).

Perhaps surprisingly, the parameters of a consteval function are not constexpr (even though consteval functions can only be evaluated at compile-time). This decision was made for the sake of consistency.



Using consteval to make constexpr execute at compile-time C++20

The downside of consteval functions is that such functions can’t evaluate at runtime, making them less flexible than constexpr functions, which can do either. Therefore, it would still be useful to have a convenient way to force constexpr functions to evaluate at compile-time (even when the return value is being used where a constant expression is not required), so that we could have compile-time evaluation when possible, and runtime evaluation when we can’t.

Consteval functions provides a way to make this happen, using a neat helper function:

```cpp
#include <iostream>

// Uses abbreviated function template (C++20) and `auto` return type to make this function work with any type of value
// See 'related content' box below for more info (you don't need to know how these work to use this function)
consteval auto compileTimeEval(auto value)
{
    return value;
}

constexpr int greater(int x, int y) // function is constexpr
{
    return (x > y ? x : y);
}

int main()
{
    std::cout << greater(5, 6) << '\n';                  // may or may not execute at compile-time
    std::cout << compileTimeEval(greater(5, 6)) << '\n'; // will execute at compile-time

    int x { 5 };
    std::cout << greater(x, 6) << '\n';                  // we can still call the constexpr version at runtime if we wish

    return 0;
}
```

Copy

This works because consteval functions require constant expressions as arguments -- therefore, if we use the return value of a constexpr function as an argument to a consteval function, the constexpr function must be evaluated at compile-time! The consteval function just returns this argument as its own return value, so the caller can still use it.

Note that the consteval function returns by value. While this might be inefficient to do at runtime (if the value was some type that is expensive to copy, e.g. std::string), in a compile-time context, it doesn’t matter because the entire call to the consteval function will simply be replaced with the calculated return value.




```cpp
#include <iostream>

constexpr int goo(int c) // goo() is now constexpr
{
    return c;
}

constexpr int foo(int b) // b is not a constant expression within foo()
{
    return goo(b);       // if foo() is resolved at compile-time, then `goo(b)` can also be resolved at compile-time
}

int main()
{
    std::cout << foo(5);

    return 0;
}
```



A constexpr function can call a non-constexpr function


Summary:

consteval makes it so it HAS to be evaulated at compile time else an error will occur

constexpr trys it at compile time but if it fails it works at runtime aswell