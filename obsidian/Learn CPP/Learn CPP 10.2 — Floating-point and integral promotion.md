
In lesson [4.3 -- Object sizes and the sizeof operator](https://www.learncpp.com/cpp-tutorial/object-sizes-and-the-sizeof-operator/), we noted that C++ has minimum size guarantees for each of the fundamental types. However, the actual size of these types can vary based on the compiler and architecture.

This variability was allowed so that the `int` and `double` data types could be set to the size that maximizes performance on a given architecture. For example, a 32-bit computer will typically be able to process 32-bits of data at a time. In such cases, an `int` would likely be set to a width of 32-bits, since this is the “natural” size of the data that the CPU operates on (and likely to be the most performant).



A reminder

The number of bits a data type uses is called its width. A wider data type is one that uses more bits, and a narrower data type is one that uses less bits.

But what happens when we want our 32-bit CPU to modify an 8-bit value (such as a `char`) or a 16-bit value? Some 32-bit processors (such as 32-bit x86 CPUs) can manipulate 8-bit or 16-bit values directly. However, doing so is often slower than manipulating 32-bit values! Other 32-bit CPUs (like 32-bit PowerPC CPUs), can only operate on 32-bit values, and additional tricks must be employed to manipulate narrower values.




Numeric promotion

Because C++ is designed to be portable and performant across a wide range of architectures, the language designers did not want to assume a given CPU would be able to efficiently manipulate values that were narrower than the natural data size for that CPU.

To help address this challenge, C++ defines a category of type conversions informally called the `numeric promotions`. A **numeric promotion** is the type conversion of certain narrower numeric types (such as a `char`) to certain wider numeric types (typically `int` or `double`) that can be processed efficiently.

All numeric promotions are value-preserving. A **value-preserving conversion** (also called a **safe conversion**) is one where every possible source value can be converted into an equal value of the destination type.

Because promotions are safe, the compiler will freely use numeric promotion as needed, and will not issue a warning when doing so.


Numeric promotion reduces redundancy

Numeric promotion solves another problem as well. Consider the case where you wanted to write a function to print a value of type `int`:

```cpp
#include <iostream>

void printInt(int x)
{
    std::cout << x << '\n';
}
```

Copy

While this is straightforward, what happens if we want to also be able to print a value of type `short`, or type `char`? If type conversions did not exist, we’d have to write a different print function for `short` and another one for `char`. And don’t forget another version for `unsigned char`, `signed char`, `unsigned short`, `wchar_t`, `char8_t`, `char16_t`, and `char32_t`! You can see how this quickly becomes unmanageable.

Numeric promotion comes to the rescue here: we can write functions that have `int` and/or `double` parameters (such as the `printInt()` function above). That same code can then be called with arguments of types that can be numerically promoted to match the types of the function parameters.

For example

```
#include <iostream>


void printInt(int x)
{
    std::cout << x << '\n';
}

int main() {
    printInt('a');
}
```

this will print 97 which is the ASCII number for a lowercase a :-3


Numeric promotion categories

The numeric promotion rules are divided into two subcategories: `integral promotions` and `floating point promotions`. Only the conversions listed in these categories are considered to be numeric promotions.

Floating point promotions

We’ll start with the easier one.

Using the **floating point promotion** rules, a value of type `float` can be converted to a value of type `double`.

This means we can write a function that takes a `double` and then call it with either a `double` or a `float` value:

```cpp
#include <iostream>

void printDouble(double d)
{
    std::cout << d << '\n';
}

int main()
{
    printDouble(5.0); // no conversion necessary
    printDouble(4.0f); // numeric promotion of float to double

    return 0;
}
```

Copy

In the second call to `printDouble()`, the `float` literal `4.0f` is promoted into a `double`, so that the type of argument matches the type of the function parameter.


*remember the f after the number tells the compiler its a float not a double*


Integral promotions

The integral promotion rules are more complicated.

Using the **integral promotion** rules, the following conversions can be made:

- signed char or signed short can be converted to int.
- unsigned char, char8_t, and unsigned short can be converted to int if int can hold the entire range of the type, or unsigned int otherwise.
- If char is signed by default, it follows the signed char conversion rules above. If it is unsigned by default, it follows the unsigned char conversion rules above.
- bool can be converted to int, with false becoming 0 and true becoming 1.

Assuming an 8 bit byte and an `int` size of 4 bytes or larger (which is typical these days), the above basically means that `bool`, `char`, `signed char`, `unsigned char`, `signed short`, and `unsigned short` all get promoted to `int`.

There are a few other integral promotion rules that are used less often. These can be found at [https://en.cppreference.com/w/cpp/language/implicit_conversion#Integral_promotion](https://en.cppreference.com/w/cpp/language/implicit_conversion#Integral_promotion).

In most cases, this lets us write a function taking an `int` parameter, and then use it with a wide variety of other integral types. For example:

```cpp
#include <iostream>

void printInt(int x)
{
    std::cout << x << '\n';
}

int main()
{
    printInt(2);

    short s{ 3 }; // there is no short literal suffix, so we'll use a variable for this one
    printInt(s); // numeric promotion of short to int

    printInt('a'); // numeric promotion of char to int
    printInt(true); // numeric promotion of bool to int

    return 0;
}
```

Copy

There are two things worth noting here. First, on some architectures (e.g. with 2 byte ints) it is possible for some of the unsigned integral types to be promoted to `unsigned int` rather than `int`.

Second, some narrower unsigned types (such as `unsigned char`) may be promoted to larger signed types (such as `int`). So while integral promotion is value-preserving, it does not necessarily preserve the signedness (signed/unsigned) of the type.




Not all widening conversions are numeric promotions

Some widening type conversions (such as `char` to `short`, or `int` to `long`) are not considered to be numeric promotions in C++ (they are `numeric conversions`, which we’ll cover shortly in lesson [10.3 -- Numeric conversions](https://www.learncpp.com/cpp-tutorial/numeric-conversions/)). This is because such conversions do not assist in the goal of converting smaller types to larger types that can be processed more efficiently.

The distinction is mostly academic. However, in certain cases, the compiler will favor numeric promotions over numeric conversions. We’ll see examples where this makes a difference when we cover function overload resolution (in upcoming lesson [11.3 -- Function overload resolution and ambiguous matches](https://www.learncpp.com/cpp-tutorial/function-overload-resolution-and-ambiguous-matches/)).