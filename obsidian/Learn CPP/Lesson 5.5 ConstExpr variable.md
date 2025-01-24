As we have established constant expressions are desirable as they Make the program run faster and optimize it during compile time



We also convered that C++ has two types of variables. Compile time constant variables and runtime constant variables. Only compile time constants can be used in constant expressions. Runtime const variables and non const variables cannot be. 


Since compile-time constant variables have no real downside we typically want to use compile time constants when possible.


## the compile time const challenge

In the prior lesson 5.4 we discussed how one way to make a compile time const variable is to use the const keyword. If the const variable has the integral type and a constant expression initalizer its a compile time constant all other const variables are treated as runtime constants

However, this method has two challenges.

First, when using `const`, our integral variables could end up as either a compile-time const or a runtime const, depending on whether the initializer is a constant expression or not. In some cases, this can make it hard to tell whether the const variable is actually a compile-time constant or not.

For example:

```cpp
int a { 5 };       // not const at all
const int b { a }; // obviously a runtime const (since initializer is non-const)
const int c { 5 }; // obviously a compile-time const (since initializer is a constant expression)

const int d { someVar };    // not obvious whether this is a runtime or compile-time const
const int e { getValue() }; // not obvious whether this is a runtime or compile-time const
```

In the above example, both `d` and `e` could be either a runtime constant or a compile-time constant depending on how `someVar` and `getValue()` are defined. It’s not clear until we hunt down the definitions for those identifiers (which may require hunting down the definition of the initializers for those variables!)

Second, this use of `const` to create compile-time constant variables does not extend to non-integral variables. And there are many cases where we would like non-integral variables to be compile-time constants too.

The `constexpr` keyword

Fortunately, we can enlist the compiler’s help to ensure we get a compile-time constant variable where we desire one. To do so, we use the `constexpr` keyword (which is shorthand for “constant expression”) instead of `const` in a variable’s declaration. A **constexpr** variable is always a compile-time constant. As a result, a constexpr variable must be initialized with a constant expression, otherwise a compilation error will result.

For example:

```cpp
#include <iostream>

// The return value of a non-constexpr function is not a constant expression
int five()
{
    return 5;
}

int main()
{
    constexpr double gravity { 9.8 }; // ok: 9.8 is a constant expression
    constexpr int sum { 4 + 5 };      // ok: 4 + 5 is a constant expression
    constexpr int something { sum };  // ok: sum is a constant expression

    std::cout << "Enter your age: ";
    int age{};
    std::cin >> age;

    constexpr int myAge { age };      // compile error: age is not a constant expression
    constexpr int f { five() };       // compile error: return value of five() is not a constant expression

    return 0;
}
```

Because functions normally execute at runtime, the return value of a function is not a constant expression (even when the value returned by the return statement is). This is why `five()` is not a legal initialization value for `constexpr int f`.


The meaning of const vs constexpr for variables

For variables:

- `const` means that the value of an object cannot be changed after initialization. The value of the initializer may be known at compile-time or runtime. The const object can be evaluated at runtime.
- `constexpr` means that the object can be used in a constant expression. The value of the initializer must be known at compile-time. The constexpr object can be evaluated at runtime or compile-time.

Constexpr variables are implicitly const. Const variables are not implicitly constexpr (except for const integral variables with a constant expression initializer).

Although a variable can be defined as both `constexpr` and `const`, in most cases this is redundant, and we only need to use either `const` or `constexpr`.



Best practice

Any constant variable whose initializer is a constant expression should be declared as `constexpr`.

Any constant variable whose initializer is not a constant expression (making it a runtime constant) should be declared as `const`.

Caveat: In the future we will discuss some types that are not fully compatible with `constexpr` (including `std::string`, `std::vector`, and other types that use dynamic memory allocation). For constant objects of these types, either use `const` instead of `constexpr`, or pick a different type that is constexpr compatible (e.g. `std::string_view` or `std::array`).


Const and constexpr function parameters

Normal function calls are evaluated at runtime, with the supplied arguments being used to initialize the function’s parameters. Because the initialization of function parameters happens at runtime, this leads to two consequences:

1. `const` function parameters are treated as runtime constants (even when the supplied argument is a compile-time constant).
2. Function parameters cannot be declared as `constexpr`, since their initialization value isn’t determined until runtime.

Nomenclature recap

|Term|Definition|
|---|---|
|Compile-time constant|A value or non-modifiable object whose value must be known at compile time (e.g. literals and constexpr variables).|
|Constexpr|Keyword that declares variables as compile-time constants (and functions that can be evaluated at compile-time). Informally, shorthand for “constant expression”.|
|Constant expression|An expression that contains only compile-time constants and operators/functions that support compile-time evaluation.|
|Runtime expression|An expression that is not a constant expression.|
|Runtime constant|A value or non-modifiable object that is not a compile-time constant.|
