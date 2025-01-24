

Consider a case where you’re going to go to the market, and your roommate tells you, “if they have strawberries on sale, buy some”. This is a conditional statement, meaning that you’ll execute some action (“buy some”) only if the condition (“they have strawberries on sale”) is true.

Such conditions are common in programming, as they allow us to implement conditional behavior into our programs. The simplest kind of conditional statement in C++ is called an _if statement_. An **if statement** allows us to execute one (or more) lines of code only if some condition is true.

The simplest _if statement_ takes the following form:

if (condition) true_statement;

For readability, this is more often written as following:

```
if (condition)
    true_statement;

```

A **condition** (also called a **conditional expression**) is an expression that evaluates to a Boolean value.

If the _condition_ of an _if statement_ evaluates to Boolean value _true_, then _true_statement_ is executed. If the _condition_ instead evaluates to Boolean value _false_, then _true_statement_ is skipped.


If-statements and early returns

A return statement that is not the last statement in a function is called an **early return**. Such a statement will cause the function to return to the caller when the return statement is executed (before the function would otherwise return to the caller, hence, “early”).

An unconditional early return is not useful:

```cpp
void print()
{
    std::cout << "A" << '\n';

    return; // the function will always return to the caller here

    std::cout << "B" << '\n'; // this will never be printed
}
```

Copy

Since `std::cout << "B" << '\n';` will never be executed, we might as well remove it, and then our `return` statement is no longer early.

However, when combined with if-statements, early returns provide a way to conditionalize the return value of our function.

```cpp
#include <iostream>

// returns the absolute value of x
int abs(int x)
{
    if (x < 0)
        return -x; // early return (only when x < 0)

    return x;
}

int main()
{
    std::cout << abs(4) << '\n'; // prints 4
    std::cout << abs(-3) << '\n'; // prints 3

    return 0;
}
```

Copy

When `abs(4)` is called, `x` has value `4`. `if (x < 0)` is false, so the early return does not execute. The function returns `x` (value `4`) to the caller at the end of the function.

When `abs(-3)` is called, `x` has value `-3`. `if (x < 0)` is true, so the early return executes. The function returns `-x` (value `3`) to the caller at this point.

Historically, early returns were frowned upon. However, in modern programming they are more accepted, particularly when they can be used to make a function simpler, or are used to abort a function early due to some error condition.



An early return is a return statement that occurs before the last line of a function. It causes the function to return to the caller immediately.


