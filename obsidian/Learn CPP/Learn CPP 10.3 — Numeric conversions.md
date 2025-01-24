
In the previous lesson ([10.2 -- Floating-point and integral promotion](https://www.learncpp.com/cpp-tutorial/floating-point-and-integral-promotion/)), we covered numeric promotions, which are conversions of specific narrower numeric types to wider numeric types (typically `int` or `double`) that can be processed efficiently.

C++ supports another category of numeric type conversions, called **numeric conversions**. These numeric conversions cover additional type conversions between fundamental types.




Key insight

Any type conversion covered by the numeric promotion rules ([10.2 -- Floating-point and integral promotion](https://www.learncpp.com/cpp-tutorial/floating-point-and-integral-promotion/)) is called a numeric promotion, not a numeric conversion.



There are five basic types of numeric conversions.

1. Converting an integral type to any other integral type (excluding integral promotions):

```cpp
short s = 3; // convert int to short
long l = 3; // convert int to long
char ch = s; // convert short to char
unsigned int u = 3; // convert int to unsigned int
```



2. Converting a floating point type to any other floating point type (excluding floating point promotions):

```cpp
float f = 3.0; // convert double to float
long double ld = 3.0; // convert double to long double
```



3. Converting a floating point type to any integral type:

```cpp
int i = 3.5; // convert double to int
```



4. Converting an integral type to any floating point type:

```cpp
double d = 3; // convert int to double
```



5. Converting an integral type or a floating point type to a bool:

```cpp
bool b1 = 3; // convert int to bool
bool b2 = 3.0; // convert double to bool
```



Safe and unsafe conversions

Unlike numeric promotions (which are always value-preserving and thus “safe”), many numeric conversions are unsafe. An **unsafe conversion** is one where at least one value of the source type cannot be converted into an equal value of the destination type.

Numeric conversions fall into three general safety categories:

1. _Value-preserving conversions_ are safe numeric conversions where the destination type can exactly represent all possible values in the source type.

For example, `int` to `long` and `short` to `double` are safe conversions, as the source value can always be converted to an equal value of the destination type.

```cpp
int main()
{
    int n { 5 };
    long l = n; // okay, produces long value 5

    short s { 5 };
    double d = s; // okay, produces double value 5.0

    return 0;
}
```

Copy

Compilers will typically not issue warnings for implicit value-preserving conversions.

A value converted using a value-preserving conversion can always be converted back to the source type, resulting in a value that is equivalent to the original value:

```cpp
#include <iostream>

int main()
{
    int n = static_cast<int>(static_cast<long>(3)); // convert int 3 to long and back
    std::cout << n << '\n';                         // prints 3

    char c = static_cast<char>(static_cast<double>('c')); // convert 'c' to double and back
    std::cout << c << '\n';                               // prints 'c'

    return 0;
}
```

Copy

2. _Reinterpretive conversions_ are unsafe numeric conversions where the converted value may be different than the source value, but no data is lost. Signed/unsigned conversions fall into this category.

For example, when converting a `signed int` to an `unsigned int`:

```cpp
int main()
{
    int n1 { 5 };
    unsigned int u1 { n1 }; // okay: will be converted to unsigned int 5 (value preserved)

    int n2 { -5 };
    unsigned int u2 { n2 }; // bad: will result in large integer outside range of signed int

    return 0;
}
```

Copy

In the case of `u1`, the signed int value `5` is converted to unsigned int value `5`. Thus, the value is preserved in this case.

In the case of `u2`, the signed int value `-5` is converted to an unsigned int. Since an unsigned int can’t represent negative numbers, the result will be modulo wrapped to a large integral value that is outside the range of a signed int. The value is not preserved in this case.

Such value changes are typically undesirable, and will often cause the program to exhibit unexpected or implementation-defined behavior.



Related content

We discuss how out-of-range values are converted between signed and unsigned types in lesson [4.12 -- Introduction to type conversion and static_cast](https://www.learncpp.com/cpp-tutorial/introduction-to-type-conversion-and-static_cast/).


Unsafe conversions should be avoided as much as possible. However, this is not always possible. When unsafe conversions are used, it is most often when:

- We can constrain the values to be converted to just those that can be converted to equal values. For example, an `int` can be safely converted to an `unsigned int` when we can guarantee that the `int` is non-negative.
- We don’t mind that some data is lost because it is not relevant. For example, converting an `int` to a `bool` results in the loss of data, but we’re typically okay with this because we’re just checking if the `int` has value `0` or not.




More on numeric conversions

The specific rules for numeric conversions are complicated and numerous, so here are the most important things to remember.

- In _all_ cases, converting a value into a type whose range doesn’t support that value will lead to results that are probably unexpected. For example:

```cpp
int main()
{
    int i{ 30000 };
    char c = i; // chars have range -128 to 127

    std::cout << static_cast<int>(c) << '\n';

    return 0;
}
```

Copy

In this example, we’ve assigned a large integer to a variable with type `char` (that has range -128 to 127). This causes the char to overflow, and produces an unexpected result:

48

- Remember that overflow is well-defined for unsigned values and produces undefined behavior for signed values.
- Converting from a larger integral or floating point type to a smaller type from the same family will generally work so long as the value fits in the range of the smaller type. For example:

```cpp
int i{ 2 };
short s = i; // convert from int to short
std::cout << s << '\n';

double d{ 0.1234 };
float f = d;
std::cout << f << '\n';
```

Copy

This produces the expected result:

2
0.1234

- In the case of floating point values, some rounding may occur due to a loss of precision in the smaller type. For example:

```cpp
float f = 0.123456789; // double value 0.123456789 has 9 significant digits, but float can only support about 7
std::cout << std::setprecision(9) << f << '\n'; // std::setprecision defined in iomanip header
```

Copy

In this case, we see a loss of precision because the `float` can’t hold as much precision as a `double`:

0.123456791

- Converting from an integer to a floating point number generally works as long as the value fits within the range of the floating point type. For example:

```cpp
int i{ 10 };
float f = i;
std::cout << f << '\n';
```

Copy

This produces the expected result:

10

- Converting from a floating point to an integer works as long as the value fits within the range of the integer, but any fractional values are lost. For example:

```cpp
int i = 3.5;
std::cout << i << '\n';
```

Copy

In this example, the fractional value (.5) is lost, leaving the following result:

3

While the numeric conversion rules might seem scary, in reality the compiler will generally warn you if you try to do something dangerous (excluding some signed/unsigned conversions).