

Implicit type conversion

Consider the following program:

```cpp
#include <iostream>

void print(double x) // print takes a double parameter
{
	std::cout << x << '\n';
}

int main()
{
	print(5); // what happens when we pass an int value?

	return 0;
}
```

Copy

In the above example, the `print()` function has a parameter of type `double` but the caller is passing in the value `5` which is of type `int`. What happens in this case?

In most cases, C++ will allow us to convert values of one fundamental type to another fundamental type. The process of converting a value from one type to another type is called **type conversion**. Thus, the int argument `5` will be converted to double value `5.0` and then copied into parameter `x`. The `print()` function will print this value, resulting in the following output:
5

A reminder

By default, floating point values whose decimal part is 0 print without the decimal places (e.g. `5.0` prints as `5`).


When the compiler does type conversion on our behalf without us explicitly asking, we call this **implicit type conversion**. The above example illustrates this -- nowhere do we explicitly tell the compiler to convert integer value `5` to double value `5.0`. Rather, the function is expecting a double value, and we pass in an integer argument. The compiler will notice the mismatch and implicitly convert the integer to a double.

Here’s a similar example where our argument is an int variable instead of an int literal:

```cpp
#include <iostream>

void print(double x) // print takes a double parameter
{
	std::cout << x << '\n';
}

int main()
{
	int y { 5 };
	print(y); // y is of type int

	return 0;
}
```

Copy

This works identically to the above. The value held by int variable `y` (`5`) will be converted to double value `5.0`, and then copied into parameter `x`.



## type conversion produces new value


Even though its called a conversion a type conversion does not actually change the value or type of the value being converted instead the value to be converted is used as input and the conversion results in a new value of the target type via direct initalization


In the above example, the conversion does not change variable `y` from type `int` to `double`. Instead, the conversion uses the value of `y` (`5`) as input to create a new double value (`5.0`). This double value is then passed to function `print`.

Key insight

Type conversion uses direct initialization to produce a new value of the target type from a value of a different type.



Implicit type conversion warnings

Although implicit type conversion is sufficient for most cases where type conversion is needed, there are a few cases where it is not. Consider the following program, which is similar to the example above:

```cpp
#include <iostream>

void print(int x) // print now takes an int parameter
{
	std::cout << x << '\n';
}

int main()
{
	print(5.5); // warning: we're passing in a double value

	return 0;
}
```

Copy

In this program, we’ve changed `print()` to take an `int` parameter, and the function call to `print()` is now passing in `double` value `5.5`. Similar to the above, the compiler will use implicit type conversion in order to convert double value `5.5` into a value of type `int`, so that it can be passed to function `print()`.

Unlike the initial example, when this program is compiled, your compiler will generate some kind of a warning about a possible loss of data. And because you have “treat warnings as errors” turned on (you do, right?), your compiler will abort the compilation process.

Tip

You’ll need to disable “treat warnings as errors” temporarily if you want to compile this example. See lesson [0.11 -- Configuring your compiler: Warning and error levels](https://www.learncpp.com/cpp-tutorial/configuring-your-compiler-warning-and-error-levels/) for more information about this setting.

When compiled and run, this program prints the following:

5

Note that although we passed in value `5.5`, the program printed `5`. Because integral values can’t hold fractions, when double value `5.5` is implicitly converted to an `int`, the fractional component is dropped, and only the integral value is retained.

Because converting a floating point value to an integral value results in any fractional component being dropped, the compiler will warn us when it does an implicit type conversion from a floating point to an integral value. This happens even if we were to pass in a floating point value with no fractional component, like `5.0` -- no actual loss of value occurs during the conversion to integral value `5` in this specific case, but the compiler may still warn us that the conversion is unsafe.

Key insight

Some type conversions are always safe to make (such as `int` to `double`), whereas others may result in the value being changed during conversion (such as `double` to `int`). Unsafe implicit conversions will typically either generate a compiler warning, or (in the case of brace initialization) an error.

This is one of the primary reasons brace initialization is the preferred initialization form. Brace initialization will ensure we don’t try to initialize a variable with an initializer that will lose value when it is implicitly type converted:

```cpp
int main()
{
    double d { 5 }; // okay: int to double is safe
    int x { 5.5 }; // error: double to int not safe

    return 0;
}
```

Copy

Related content

Implicit type conversion is a meaty topic. We dig into this topic in more depth in future lessons, starting with lesson [10.1 -- Implicit type conversion](https://www.learncpp.com/cpp-tutorial/implicit-type-conversion/).






## introduction to explicit type conversion via the static_cast operator


Well what if the compiler doesnt convert the type for us. This is called explicit type conversion.


What if we wanted to intentionally wanted to pass a double value to a function taking an integer knowing it will drop the fractional component and we dont want to turn off treat warning as errors. 


C++ supports a second method of type conversion called explicit type conversion allows us to tell the compiler to convert a value from one type to another


To perform an explicit type conversion, in most cases we will use the static_cast operator the syntax for this looks a little funny tho

```
static_cast<new_type>(expression)
```
static_cast takes the value from an expression as input, and returns that value converted into the type specified by _new_type_ (e.g. int, bool, char, double).

Key insight

Whenever you see C++ syntax (excluding the preprocessor) that makes use of angled brackets (<>), the thing between the angled brackets will most likely be a type. This is typically how C++ deals with code that need a parameterized type.

Let’s update our prior program using `static_cast`:

```cpp
#include <iostream>

void print(int x)
{
	std::cout << x << '\n';
}

int main()
{
	print( static_cast<int>(5.5) ); // explicitly convert double value 5.5 to an int

	return 0;
}
```

Copy

Because we’re now explicitly requesting that double value `5.5` be converted to an `int` value, the compiler will not generate a warning about a possible loss of data upon compilation (meaning we can leave “treat warnings as errors” enabled).

Related content

C++ supports other types of casts. We talk more about the different types of casts in future lesson [10.6](https://www.learncpp.com/cpp-tutorial/explicit-type-conversion-casting-and-static-cast/)



Say we wanted to Print the Decimal value of an ASCII char well lets just do this

```
int main() {
	char b{ 'h' };

	std::cout << static_cast<int>(b) << '\n';

}
```



or we could do it the other way around and convert a decimal char value to the letter.


It’s worth noting that the argument to _static_cast_ evaluates as an expression. When we pass in a variable, that variable is evaluated to produce its value, and that value is then converted to the new type. The variable itself is _not_ affected by casting its value to a new type. In the above case, variable `ch` is still a char, and still holds the same value even after we’ve cast its value to an `int`.



Sign conversions using static_cast

Signed integral values can be converted to unsigned integral values, and vice-versa, using a static cast.

If the value being converted can be represented in the destination type, the converted value will remain unchanged (only the type will change). For example:

as long as the value is in the range of both unsigned and signed int meaning its not negative the value can be converted



If the value being converted cannot be represented in the destination type:

- If the destination type is unsigned, the value will be modulo wrapped. We cover modulo wrapping in lesson [4.5 -- Unsigned integers, and why to avoid them](https://www.learncpp.com/cpp-tutorial/unsigned-integers-and-why-to-avoid-them/).
- If the destination type is signed, the value is implementation-defined prior to C++20, and will be modulo wrapped as of C++20.

Here’s an example of converting two values that are not representable in the destination type (assuming 32-bit integers):

```cpp
#include <iostream>

int main()
{
    int s { -1 };
    std::cout << static_cast<unsigned int>(s) << '\n'; // prints 4294967295

    unsigned int u { 4294967295 }; // largest 32-bit unsigned int
    std::cout << static_cast<int>(u) << '\n'; // implementation-defined prior to C++20, -1 as of C++20

    return 0;
}
```

Copy

As of C++20, this produces the result:

4294967295
-1

Signed int value `-1` cannot be represented as an unsigned int. The result modulo wraps to unsigned int value `4294967295`.

Unsigned int value `4294967295` cannot be represented as a signed int. Prior to C++20, the result is implementation defined (but will probably be `-1`). As of C++20, the result will modulo wrap to `-1`.

Warning

Converting an unsigned integral value to a signed integral value will result in implementation-defined behavior prior to C++20 if the value being converted can not be represented in the signed type.



std::int8_t and std::uint8_t likely behave like chars instead of integers

As noted in lesson [4.6 -- Fixed-width integers and size_t](https://www.learncpp.com/cpp-tutorial/fixed-width-integers-and-size-t/), most compilers define and treat `std::int8_t` and `std::uint8_t` (and the corresponding fast and least fixed-width types) identically to types `signed char` and `unsigned char` respectively. Now that we’ve covered what chars are, we can demonstrate where this can be problematic:

```cpp
#include <cstdint>
#include <iostream>

int main()
{
    std::int8_t myInt{65};      // initialize myInt with value 65
    std::cout << myInt << '\n'; // you're probably expecting this to print 65

    return 0;
}
```

Copy

Because `std::int8_t` describes itself as an int, you might be tricked into believing that the above program will print the integral value `65`. However, on most systems, this program will print `A` instead (treating `myInt` as a `signed char`). However, this is not guaranteed (on some systems, it may actually print `65`).

If you want to ensure that a `std::int8_t` or `std::uint8_t` object is treated as an integer, you can convert the value to an integer using `static_cast`:

```cpp
#include <cstdint>
#include <iostream>

int main()
{
    std::int8_t myInt{65};
    std::cout << static_cast<int>(myInt) << '\n'; // will always print 65

    return 0;
}
```

Copy

In cases where `std::int8_t` is treated as a char, input from the console can also cause problems:

```cpp
#include <cstdint>
#include <iostream>

int main()
{
    std::cout << "Enter a number between 0 and 127: ";
    std::int8_t myInt{};
    std::cin >> myInt;

    std::cout << "You entered: " << static_cast<int>(myInt) << '\n';

    return 0;
}
```

Copy

A sample run of this program:

Enter a number between 0 and 127: 35
You entered: 51

Here’s what’s happening. When `std::int8_t` is treated as a char, the input routines interpret our input as a sequence of characters, not as an integer. So when we enter `35`, we’re actually entering two chars, `'3'` and `'5'`. Because a char object can only hold one character, the `'3'` is extracted (the `'5'` is left in the input stream for possible extraction later). Because the char `'3'` has ASCII code point 51, the value `51` is stored in `myInt`, which we then print later as an int.

In contrast, the other fixed-width types will always print and input as integral values.