
Semantic errors can cause most of the same symptoms of `undefined behavior`, such as causing the program to produce the wrong results, causing erratic behavior, corrupting program data, causing the program to crash -- or they may not have any impact at all.


Conditional logic errors

One of the most common types of semantic errors is a conditional logic error. A **conditional logic error** occurs when the programmer incorrectly codes the logic of a conditional statement or loop condition. Here is a simple example:

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter an integer: ";
    int x{};
    std::cin >> x;

    if (x >= 5) // oops, we used operator>= instead of operator>
        std::cout << x << " is greater than 5\n";

    return 0;
}
```

Copy

Here’s a run of the program that exhibits the conditional logic error:

Enter an integer: 5
5 is greater than 5

When the user enters `5`, the conditional expression `x >= 5` evaluates to `true`, so the associated statement is executed.


Infinite loops

In lesson [8.8 -- Introduction to loops and while statements](https://www.learncpp.com/cpp-tutorial/introduction-to-loops-and-while-statements/), we covered infinite loops, and showed this example:

```cpp
#include <iostream>

int main()
{
    int count{ 1 };
    while (count <= 10) // this condition will never be false
    {
        std::cout << count << ' '; // so this line will repeatedly execute
    }

    std::cout << '\n'; // this line will never execute

    return 0; // this line will never execute
}
```

Copy

In this case, we forgot to increment `count`, so the loop condition will never be false, and the loop will continue to print:



Here’s another example that teachers love asking as a quiz question. What’s wrong with the following code?

```cpp
#include <iostream>

int main()
{
    for (unsigned int count{ 5 }; count >= 0; --count)
    {
        if (count == 0)
            std::cout << "blastoff! ";
        else
          std::cout << count << ' ';
    }

    std::cout << '\n';

    return 0;
}
```

Copy

This program is supposed to print `5 4 3 2 1 blastoff!`, which it does, but it doesn’t stop there. In actuality, it prints:

5 4 3 2 1 blastoff! 4294967295 4294967294 4294967293 4294967292 4294967291

and then just keeps decrementing. The program will never terminate, because `count >= 0` can never be `false` when `count` is an unsigned integer.



Incorrect operator precedence

From lesson [6.7 -- Logical operators](https://www.learncpp.com/cpp-tutorial/logical-operators/), the following program makes an operator precedence mistake:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int y{ 7 };

    if (!x > y) // oops: operator precedence issue
        std::cout << x << " is not greater than " << y << '\n';
    else
        std::cout << x << " is greater than " << y << '\n';

    return 0;
}
```

Copy

Because `logical NOT` has higher precedence than `operator>`, the conditional evaluates as if it was written `(!x) > y`, which isn’t what the programmer intended.

As a result, this program prints:

5 is greater than 7

This can also happen when mixing Logical OR and Logical AND in the same expression (Logical AND takes precedence over Logical OR). Use explicit parenthesization to avoid these kinds of errors.



Precision issues with floating point types

The following floating point variable doesn’t have enough precision to store the entire number:

```cpp
#include <iostream>

int main()
{
    float f{ 0.123456789f };
    std::cout << f << '\n';

    return 0;
}
```

Copy

Because of this lack of precision, the number is rounded slightly:

0.123457

In lesson [6.6 -- Relational operators and floating point comparisons](https://www.learncpp.com/cpp-tutorial/relational-operators-and-floating-point-comparisons/), we talked about how using `operator==` and `operator!=` can be problematic with floating point numbers due to small rounding errors (as well as what to do about it). Here’s an example:

```cpp
#include <iostream>

int main()
{
    double d{ 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 }; // should sum to 1.0

    if (d == 1.0)
        std::cout << "equal\n";
    else
        std::cout << "not equal\n";

    return 0;
}
```

Copy

This program prints:

not equal

The more arithmetic you do with a floating point number, the more it will accumulate small rounding errors.



Integer division

In the following example, we mean to do a floating point division, but because both operands are integers, we end up doing an integer division instead:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int y{ 3 };

    std::cout << x << " divided by " << y << " is: " << x / y << '\n'; // integer division

    return 0;
}
```

Copy

This prints:

5 divided by 3 is: 1

In lesson [6.2 -- Arithmetic operators](https://www.learncpp.com/cpp-tutorial/arithmetic-operators/), we showed that we can use static_cast to convert one of the integral operands to a floating point value in order to do floating point division.


Accidental null statements

In lesson [8.3 -- Common if statement problems](https://www.learncpp.com/cpp-tutorial/common-if-statement-problems/), we covered `null statements`, which are statements that do nothing.

In the below program, we only want to blow up the world if we have the user’s permission:

```cpp
#include <iostream>

void blowUpWorld()
{
    std::cout << "Kaboom!\n";
}

int main()
{
    std::cout << "Should we blow up the world again? (y/n): ";
    char c{};
    std::cin >> c;

    if (c == 'y');     // accidental null statement here
        blowUpWorld(); // so this will always execute since it's not part of the if-statement

    return 0;
}
```

Copy

However, because of an accidental `null statement`, the function call to `blowUpWorld()` is always executed, so we blow it up regardless:
its null because they ended the if statement with ;


Not using a compound statement when one is required

Another variant of the above program that always blows up the world:

```cpp
#include <iostream>

void blowUpWorld()
{
    std::cout << "Kaboom!\n";
}

int main()
{
    std::cout << "Should we blow up the world again? (y/n): ";
    char c{};
    std::cin >> c;

    if (c == 'y')
        std::cout << "Okay, here we go...\n";
        blowUpWorld(); // Will always execute.  Should be inside compound statement.

    return 0;
}
```

Copy

This program prints:

Should we blow up the world again? (y/n): n
Kaboom!

A `dangling else` (covered in lesson [8.3 -- Common if statement problems](https://www.learncpp.com/cpp-tutorial/common-if-statement-problems/)) also falls into this category.


