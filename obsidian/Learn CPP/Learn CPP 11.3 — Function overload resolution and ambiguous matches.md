

However, having a set of differentiated overloaded functions is only half of the picture. When any function call is made, the compiler must also ensure that a matching function declaration can be found.

With non-overloaded functions (functions with unique names), there is only one function that can potentially match a function call. That function either matches (or can be made to match after type conversions are applied), or it doesn’t (and a compile error results). With overloaded functions, there can be many functions that can potentially match a function call. Since a function call can only resolve to one of them, the compiler has to determine which overloaded function is the best match. The process of matching function calls to a specific overloaded function is called **overload resolution**.

In simple cases where the type of the function arguments and type of the function parameters match exactly, this is (usually) straightforward:

```cpp
#include <iostream>

void print(int x)
{
     std::cout << x << '\n';
}

void print(double d)
{
     std::cout << d << '\n';
}

int main()
{
     print(5); // 5 is an int, so this matches print(int)
     print(6.7); // 6.7 is a double, so this matches print(double)

     return 0;
}
```

Copy

But what happens in cases where the argument types in the function call don’t exactly match the parameter types in any of the overloaded functions? For example:

```cpp
#include <iostream>

void print(int x)
{
     std::cout << x << '\n';
}

void print(double d)
{
     std::cout << d << '\n';
}

int main()
{
     print('a'); // char does not match int or double, so what happens?
     print(5L); // long does not match int or double, so what happens?

     return 0;
}
```

Copy

Just because there is no exact match here doesn’t mean a match can’t be found -- after all, a `char` or `long` can be implicitly type converted to an `int` or a `double`. But which is the best conversion to make in each case?

In this lesson, we’ll explore how the compiler matches a given function call to a specific overloaded function.


Resolving overloaded function calls

When a function call is made to an overloaded function, the compiler steps through a sequence of rules to determine which (if any) of the overloaded functions is the best match (we’ll cover these steps in the next section below).

At each step, the compiler applies a bunch of different type conversions to the argument(s) in the function call. For each conversion applied, the compiler checks if any of the overloaded functions are now a match. After all the different type conversions have been applied and checked for matches, the step is done. The result will be one of three possible outcomes:

- No matching functions were found. The compiler moves to the next step in the sequence.
- A single matching function was found. This function is considered to be the best match. The matching process is now complete, and subsequent steps are not executed.
- More than one matching function was found. The compiler will issue an ambiguous match compile error. We’ll discuss this case further in a bit.

If the compiler reaches the end of the entire sequence without finding a match, it will generate a compile error that no matching overloaded function could be found for the function call.

Therefor the code above results in a compile error.


The argument matching sequence

Step 1) The compiler tries to find an exact match. This happens in two phases. First, the compiler will see if there is an overloaded function where the type of the arguments in the function call exactly matches the type of the parameters in the overloaded functions. For example:

```cpp
void foo(int)
{
}

void foo(double)
{
}

int main()
{
    foo(0);   // exact match with foo(int)
    foo(3.4); // exact match with foo(double)

    return 0;
}
```

Copy

Because the `0` in the function call `foo(0)` is an int, the compiler will look to see if a `foo(int)` overload has been declared. Since it has, the compiler determines that `foo(int)` is an exact match.

Second, the compiler will apply a number of trivial conversions to the arguments in the function call. The **trivial conversions** are a set of specific conversion rules that will modify types (without modifying the value) for purposes of finding a match. These include:

- lvalue to rvalue conversions
- qualification conversions (e.g. non-const to const)
- non-reference to reference conversions

For example:

```cpp
void foo(const int)
{
}

void foo(const double&)
{
}

int main()
{
    int x { 1 };
    foo(x); // x trivially converted from int to const int

    double d { 2.3 };
    foo(d); // d trivially converted from double to const double&

    return 0;
}
```

Copy

In the above example, we’ve called `foo(x)`, where `x` is an `int`. The compiler will trivially convert `x` from an `int` into a `const int`, which then matches `foo(const int)`. We’ve also called `foo(d)`, where `d` is a `double`. The compiler will trivially convert `d` from a `double` to a `const double&`, which then matches `foo(const double&)`.

Matches made via the trivial conversions are considered exact matches. This means the following program results in an ambiguous match:

```cpp
void foo(int)
{
}

void foo(const int&)
{
}

int main()
{
    int x { 1 };
    foo(x); // ambiguous match with foo(int) and foo(const int&)

    return 0;
}
```

Copy

Step 2) If no exact match is found, the compiler tries to find a match by applying numeric promotion to the argument(s). In lesson ([10.1 -- Implicit type conversion](https://www.learncpp.com/cpp-tutorial/implicit-type-conversion/)), we covered how certain narrow integral and floating point types can be automatically promoted to wider types, such as `int` or `double`. If, after numeric promotion, a match is found, the function call is resolved.

For example:

```cpp
void foo(int)
{
}

void foo(double)
{
}

int main()
{
    foo('a');  // promoted to match foo(int)
    foo(true); // promoted to match foo(int)
    foo(4.5f); // promoted to match foo(double)

    return 0;
}
```

Copy

For `foo('a')`, because an exact match for `foo(char)` could not be found in the prior step, the compiler promotes the char `'a'` to an `int`, and looks for a match. This matches `foo(int)`, so the function call resolves to `foo(int)`.

Step 3) If no match is found via numeric promotion, the compiler tries to find a match by applying numeric conversions ([10.3 -- Numeric conversions](https://www.learncpp.com/cpp-tutorial/numeric-conversions/)) to the arguments.

For example:

```cpp
#include <string> // for std::string

void foo(double)
{
}

void foo(std::string)
{
}

int main()
{
    foo('a'); // 'a' converted to match foo(double)

    return 0;
}
```

Copy

In this case, because there is no `foo(char)` (exact match), and no `foo(int)` (promotion match), the `'a'` is numerically converted to a double and matched with `foo(double)`.

Key insight

Matches made by applying numeric promotions take precedence over any matches made by applying numeric conversions.

Step 4) If no match is found via numeric conversion, the compiler tries to find a match through any user-defined conversions. Although we haven’t covered user-defined conversions yet, certain types (e.g. classes) can define conversions to other types that can be implicitly invoked. Here’s an example, just to illustrate the point:

```cpp
// We haven't covered classes yet, so don't worry if this doesn't make sense
class X // this defines a new type called X
{
public:
    operator int() { return 0; } // Here's a user-defined conversion from X to int
};

void foo(int)
{
}

void foo(double)
{
}

int main()
{
    X x; // Here, we're creating an object of type X (named x)
    foo(x); // x is converted to type int using the user-defined conversion from X to int

    return 0;
}
```

Copy

In this example, the compiler will first check whether an exact match to `foo(X)` exists. We haven’t defined one. Next the compiler will check whether `x` can be numerically promoted, which it can’t. The compiler will then check if `x` can be numerically converted, which it also can’t. Finally, the compiler will then look for any user-defined conversions. Because we’ve defined a user-defined conversion from `X` to `int`, the compiler will convert `X` to an `int` to match `foo(int)`.

After applying a user-defined conversion, the compiler may apply additional implicit promotions or conversions to find a match. So if our user-defined conversion had been to type `char` instead of `int`, the compiler would have used the user-defined conversion to `char` and then promoted the result into an `int` to match.


Ambiguous matches

With non-overloaded functions, each function call will either resolve to a function, or no match will be found and the compiler will issue a compile error:


Resolving ambiguous matches

Because ambiguous matches are a compile-time error, an ambiguous match needs to be disambiguated before your program will compile. There are a few ways to resolve ambiguous matches:

1. Often, the best way is simply to define a new overloaded function that takes parameters of exactly the type you are trying to call the function with. Then C++ will be able to find an exact match for the function call.
2. Alternatively, explicitly cast the ambiguous argument(s) to match the type of the function you want to call. For example, to have `foo(0)` match `foo(unsigned int)` in the above example, you would do this:

```cpp
int x{ 0 };
foo(static_cast<unsigned int>(x)); // will call foo(unsigned int)
```

Copy

3. If your argument is a literal, you can use the literal suffix to ensure your literal is interpreted as the correct type:

```cpp
foo(0u); // will call foo(unsigned int) since 'u' suffix is unsigned int, so this is now an exact match
```

Copy

The list of the most used suffixes can be found in lesson [5.2 -- Literals](https://www.learncpp.com/cpp-tutorial/literals/).


