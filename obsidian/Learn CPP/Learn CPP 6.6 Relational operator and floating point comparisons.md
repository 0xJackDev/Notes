
**Relational operators** are operators that let you compare two values. There are 6 relational operators:

|Operator|Symbol|Form|Operation|
|---|---|---|---|
|Greater than|>|x > y|true if x is greater than y, false otherwise|
|Less than|<|x < y|true if x is less than y, false otherwise|
|Greater than or equals|>=|x >= y|true if x is greater than or equal to y, false otherwise|
|Less than or equals|<=|x <= y|true if x is less than or equal to y, false otherwise|
|Equality|==|x == y|true if x equals y, false otherwise|
|Inequality|!=|x != y|true if x does not equal y, false otherwise|

You have already seen how most of these work, and they are pretty intuitive. Each of these operators evaluates to the boolean value true (1), or false (0).

Here’s some sample code using these operators with integers:


Boolean conditional values

By default, conditions in an _if statement_ or _conditional operator_ (and a few other places) evaluate as Boolean values.

Many new programmers will write statements like this one:

```cpp
if (b1 == true) ...
```

Copy

This is redundant, as the `== true` doesn’t actually add any value to the condition. Instead, we should write:

```cpp
if (b1) ...
```

Copy

Similarly, the following:

```cpp
if (b1 == false) ...
```

Copy

is better written as:

```cpp
if (!b1) ...
```


## Comparison of calculated floating point values can be problematic

Consider the following program:

```cpp
#include <iostream>

int main()
{
    constexpr double d1{ 100.0 - 99.99 }; // should equal 0.01 mathematically
    constexpr double d2{ 10.0 - 9.99 }; // should equal 0.01 mathematically

    if (d1 == d2)
        std::cout << "d1 == d2" << '\n';
    else if (d1 > d2)
        std::cout << "d1 > d2" << '\n';
    else if (d1 < d2)
        std::cout << "d1 < d2" << '\n';

    return 0;
}
```

Copy

Variables d1 and d2 should both have value _0.01_. But this program prints an unexpected result:

d1 > d2

If you inspect the value of d1 and d2 in a debugger, you’d likely see that d1 = 0.010000000000005116 and d2 = 0.0099999999999997868. Both numbers are close to 0.01, but d1 is greater than, and d2 is less than.

Comparing floating point values using any of the relational operators can be dangerous. This is because floating point values are not precise, and small rounding errors in the floating point operands may cause them to be slightly smaller or slightly larger than expected. And this can throw off the relational operators.



Floating point less-than and greater-than

When the less-than (<), greater-than (>), less-than-equals (<=), and greater-than-equals (>=) operators are used with floating point values, they will produce a reliable answer in most cases (when the value of the operands is not similar). However, if the operands are almost identical, these operators should be considered unreliable. For example, `d1 > d2` happens to produce `true` in the above example, but could have just as easily produced `false` if the numerical errors had gone a different direction.



Floating point equality and inequality

The equality operators (== and !=) are much more troublesome. Consider operator==, which returns true only if its operands are exactly equal. Because even the smallest rounding error will cause two floating point numbers to not be equal, operator== is at high risk for returning false when a true might be expected. Operator!= has the same kind of problem.

NEVER USE == and =! to compare float values if there is any chance those floats were calculated 

There is one notable exception case to the above: It is safe to compare a floating point literal with a variable of the same type that has been initialized with a literal of the same type, so long as the number of significant digits in each literal does not exceed the minimum precision for that type. Float has a minimum precision of 6 significant digits, and double has a minimum precision of 15 significant digits.

For example, you may occasionally see a function that returns a floating point literal (typically `0.0`, or sometimes `1.0`). In such cases, it is safe to do a direct comparison against the same literal value of the same type:

```cpp
if (someFcn() == 0.0) // okay if someFcn() returns 0.0 as a literal only
    // do something
```

Copy

Instead of a literal, we can also compare a const or constexpr floating point variable that was initialized with a literal value:

```cpp
constexpr double gravity { 9.8 };
if (gravity == 9.8) // okay if gravity was initialized with a literal
    // we're on earth
```

Copy

It is mostly not safe to compare floating point literals of different types. For example, comparing `9.8f` to `9.8` will return false.


## Comparing floating point numbers (advanced / optional reading)

So how can we reasonably compare two floating point operands to see if they are equal?

The most common method of doing floating point equality involves using a function that looks to see if two numbers are _almost_ the same. If they are “close enough”, then we call them equal. The value used to represent “close enough” is traditionally called **epsilon**. Epsilon is generally defined as a small positive number (e.g. 0.00000001, sometimes written 1e-8).

New developers often try to write their own “close enough” function like this:

```cpp
#include <cmath> // for std::abs()

// absEpsilon is an absolute value
bool approximatelyEqualAbs(double a, double b, double absEpsilon)
{
    // if the distance between a and b is less than or equal to absEpsilon, then a and b are "close enough"
    return std::abs(a - b) <= absEpsilon;
}
```

Copy

std::abs() is a function in the cmath header that returns the absolute value of its argument. So `std::abs(a - b) <= absEpsilon` checks if the distance between _a_ and _b_ is less than or equal to whatever epsilon value representing “close enough” was passed in. If _a_ and _b_ are close enough, the function returns true to indicate they’re equal. Otherwise, it returns false.

While this function can work, it’s not great. An epsilon of _0.00001_ is good for inputs around _1.0_, too big for inputs around _0.0000001_, and too small for inputs like _10,000_.


This means every time we call this function, we have to pick an epsilon that’s appropriate for our inputs. If we know we’re going to have to scale epsilon in proportion to the magnitude of our inputs, we might as well modify the function to do that for us.

[Donald Knuth](https://en.wikipedia.org/wiki/Donald_Knuth), a famous computer scientist, suggested the following method in his book “The Art of Computer Programming, Volume II: Seminumerical Algorithms (Addison-Wesley, 1969)”:

```cpp
#include <algorithm> // for std::max
#include <cmath>     // for std::abs

// Return true if the difference between a and b is within epsilon percent of the larger of a and b
bool approximatelyEqualRel(double a, double b, double relEpsilon)
{
	return (std::abs(a - b) <= (std::max(std::abs(a), std::abs(b)) * relEpsilon));
}
```

Copy

In this case, instead of epsilon being an absolute number, epsilon is now relative to the magnitude of _a_ or _b_.

Let’s examine in more detail how this crazy looking function works. On the left side of the <= operator, `std::abs(a - b)` tells us the distance between _a_ and _b_ as a positive number.

On the right side of the <= operator, we need to calculate the largest value of “close enough” we’re willing to accept. To do this, the algorithm chooses the larger of _a_ and _b_ (as a rough indicator of the overall magnitude of the numbers), and then multiplies it by relEpsilon. In this function, relEpsilon represents a percentage. For example, if we want to say “close enough” means _a_ and _b_ are within 1% of the larger of _a_ and _b_, we pass in an relEpsilon of 0.01 (1% = 1/100 = 0.01). The value for relEpsilon can be adjusted to whatever is most appropriate for the circumstances (e.g. an epsilon of 0.002 means within 0.2%).

Making the `approximatelyEqual` functions constexpr Advanced

In C++23, the two `approximatelyEqual` functions can be made constexpr by adding the `constexpr` keyword:

```cpp
// C++23 version
#include <algorithm> // for std::max
#include <cmath>     // for std::abs (constexpr in C++23)

// Return true if the difference between a and b is within epsilon percent of the larger of a and b
constexpr bool approximatelyEqualRel(double a, double b, double relEpsilon)
{
	return (std::abs(a - b) <= (std::max(std::abs(a), std::abs(b)) * relEpsilon));
}

// Return true if the difference between a and b is less than or equal to absEpsilon, or within relEpsilon percent of the larger of a and b
constexpr bool approximatelyEqualAbsRel(double a, double b, double absEpsilon, double relEpsilon)
{
    // Check if the numbers are really close -- needed when comparing numbers near zero.
    if (std::abs(a - b) <= absEpsilon)
        return true;

    // Otherwise fall back to Knuth's algorithm
    return approximatelyEqualRel(a, b, relEpsilon);
}
```