

## The-as if rule

In C++, compilers are given a lot of leeway to optmize programs. The as-if rule says that the compiler can modify a program however it likes in order to produce more optmized code, so long as those modifications dont affect the programs observable behavior.

Exactly how a compiler optimizes a given program is up to the compiler itself. However there are things we can do to help the compiler optimize better.


A optimization oppuritinity
Consider the following program

```cpp
#include <iostream>

int main()
{
	int x { 3 + 4 };
	std::cout << x << '\n';

	return 0;
}
```

The output is 7 pretty straightforward right??

well there's actually a interesting optimization possibility hidden optimization possibility within. 


If this program was compiled exactly as it was written the compiler would generate a executable that calculates the result of 3 + 4 at runtime when the program is run. If the program were executed a million times, 3 + 4 

Because the result of `3 + 4` never changes (it is always `7`), re-calculating this result every time the program is run is wasteful.


Compile-time evaluation of expressions

Modern C++ compilers are able to evaluate some expressions at compile-time. When this occurs, the compiler can replace the expression with the result of the expression.

For example, the compiler could optimize the above example to this:

```cpp
#include <iostream>

int main()
{
	int x { 7 };
	std::cout << x << '\n';

	return 0;
}
```

Copy

This program produces the same output (`7`) as the prior version, but the resulting executable no longer needs to spend CPU cycles calculating `3 + 4` at runtime! Even better, we don’t need to do anything to enable this behavior (besides have optimizations turned on).




Key insight

Compile-time evaluation allows the compiler to do work at compile-time that would otherwise be done at runtime.

Such optimizations make our compilation take longer, but because expressions only need to be evaluated once at compile-time (rather than every time the program is run) the resulting executables are faster and use less memory.

The ability for C++ to perform compile-time evaluation is one of the most important and evolving areas of modern C++.

Author’s note

Quite a few of the next lessons deal with compile-time evaluation.

Constant expressions [](https://www.learncpp.com/cpp-tutorial/constant-expressions-and-compile-time-optimization/#constantexpressions)

One kind of expression that can always be evaluated at compile time is called a “constant expression”. The precise definition of a constant expression is complicated, so we’ll take a simplified view: A **constant expression** is an expression that contains only compile-time constants and operators/functions that support compile-time evaluation.

Author’s note

Even simpler: A constant expression is an expression where everything in the expression can be evaluated at compile-time.

A **compile-time constant** is a constant whose value _must be_ known at compile time. This includes:

- Literals (e.g. ‘5’, ‘1.2’)
- Constexpr variables (we discuss these shortly in lesson [5.5 -- Constexpr variables](https://www.learncpp.com/cpp-tutorial/constexpr-variables/))
- Const integral variables with a constant expression initializer (e.g. `const int x { 5 };`). This is a historical exception -- in modern C++, constexpr variables are preferred.
- Non-type template parameters (see [11.10 -- Non-type template parameters](https://www.learncpp.com/cpp-tutorial/non-type-template-parameters/)).
- Enumerators (see [13.2 -- Unscoped enumerations](https://www.learncpp.com/cpp-tutorial/unscoped-enumerations/)).



The most common type of operators and functions that support compile-time evaluation include:

- Arithmetic operators with operands that are compile-time constants (e.g. `1 + 2`)
- Constexpr and consteval functions (we’ll discuss these later in the chapter)

In the following example, we identify the constant expressions and non-constant expressions. We also identify which variables are non-constant, runtime constant, or compile-time constant.

```cpp
#include <iostream>

int getNumber()
{
    std::cout << "Enter a number: ";
    int y{};
    std::cin >> y;

    return y;
}

int main()
{
    // Non-const variables are always non-constants:
    int a { 5 };                 // 5 is a constant expression
    double b { 1.2 + 3.4 };      // 1.2 + 3.4 is a constant expression

    // Const integral variables with a constant expression initializer are compile-time constants:
    const int c { 5 };           // 5 is a constant expression
    const int d { c };           // c is a constant expression
    const long e { c + 2 };      // c + 2 is a constant expression

    // Other const variables are runtime constants:
    const int f { a };           // a is not a constant expression
    const int g { a + 1 };       // a + 1 is not a constant expression
    const int h { a + c };       // a + c is not a constant expression
    const int i { getNumber() }; // getNumber() is not a constant expression

    const double j { b };        // b is not a constant expression
    const double k { 1.2 };      // 1.2 is a constant expression

    return 0;
}
```


An expression that is not a constant expression is sometimes called a **runtime expression**. For example, `std::cout << x << '\n'` is a runtime expression, both because `x` is not a compile-time constant, and because `operator<<` doesn’t support compile-time evaluation when used for output (since output can’t be done at compile-time).


Why we care about constant expressions [](https://www.learncpp.com/cpp-tutorial/constant-expressions-and-compile-time-optimization/#whywecare)

Constant expressions are useful for (at least) three reasons:

- Constant expressions are _always_ eligible for compile-time evaluation, meaning they are more likely to be optimized at compile-time. This produces faster and smaller code.
- With runtime expressions, only the type of the expression is known at compile-time. With constant expression, both the type AND the value of the expression is known at compile-time. This allows us to do compile-time sanity checking of those values. If such a value does not meet our requirements, we can fail the build, allowing us to identify and fix the issue immediately. The result is code that is safer, easier to test, and more difficult to misuse.
- Certain C++ features that we’ll cover in future lessons require constant expressions (see below).

For advanced readers

A few common cases where a constant expression is required:

- The initializer of a constexpr variable ([5.5 -- Constexpr variables](https://www.learncpp.com/cpp-tutorial/constexpr-variables/)).
- A non-type template argument ([11.10 -- Non-type template parameters](https://www.learncpp.com/cpp-tutorial/non-type-template-parameters/)).
- The defined length of a `std::array` ([17.1 -- Introduction to std::array](https://www.learncpp.com/cpp-tutorial/introduction-to-stdarray/)) or a C-style array ([17.7 -- Introduction to C-style arrays](https://www.learncpp.com/cpp-tutorial/introduction-to-c-style-arrays/)).



Partial optimization of constant subexpressions

Now consider the following example:

```cpp
#include <iostream>

int main()
{
	std::cout << 3 + 4 << '\n';

	return 0;
}
```

Copy

The full expression `std::cout << 3 + 4 << '\n';` is a runtime expression because output can only be done at runtime. But notice that the full expression contains constant subexpression `3 + 4`.



The compiler can optimize code and completly remove variables and replace them say we have a const variable named x that is 3+4 well the compiler sees its a const and knows that it wont be change so it can just make that const x {7};  

Ranking variables by the likelihood of the compiler being able to optimize them:

- Compile-time constant variables (always eligible to be optimized)
- Runtime constant variables
- Non-const variables (likely optimized in simple cases only)



Optimization can make programs harder to debug

When the compiler optimizes a program, variables, expressions, statements, and function calls may be rearranged, altered, replaced with a value, or even removed entirely. Such changes can make it hard to debug a program effectively.

At runtime, it can be hard to debug compiled code that no longer correlates very well with the original source code. For example, if you try to watch a variable that has been optimized out, the debugger won’t be able to locate the variable. If you try to step into a function that has been optimized away, the debugger will simply skip over it. So if you are debugging your code and the debugger is behaving strangely, this is the most likely reason.

At compile-time, we have little visibility and few tools to help us understand what the compiler is even doing. If a variable or expression is replaced with a value, and that value is wrong, how do we even go about debugging it? This is an ongoing challenge.

To help minimize such issues, debug builds will typically turn down (or turn off) optimizations, so that the compiled code will more closely match the source code.



Debug builds typically disable optmization



you can also have half statements that where the runtime is constant expression is constant like 1.0 but the variable isnt declared as a const so it isnt const or for example

const int f {d+ 2}; 

well in this case the variable is constant but the expression isnt since the value b can change.

