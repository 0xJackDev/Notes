Nested if statements and the dangling else problem

It is possible to nest `if statements` within other `if statements`:


Now consider the following program:

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter a number: ";
    int x{};
    std::cin >> x;

    if (x >= 0) // outer if statement
        // it is bad coding style to nest if statements this way
        if (x <= 20) // inner if statement
            std::cout << x << " is between 0 and 20\n";

    // which if statement does this else belong to?
    else
        std::cout << x << " is negative\n";

    return 0;
}
```

Copy

The above program introduces a source of potential ambiguity called a **dangling else** problem. Is the `else statement` in the above program matched up with the outer or inner `if statement`?

The answer is that an `else statement` is paired up with the last unmatched `if statement` in the same block. Thus, in the program above, the `else` is matched up with the inner `if statement`, as if the program had been written like this:

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter a number: ";
    int x{};
    std::cin >> x;

    if (x >= 0) // outer if statement
    {
        if (x <= 20) // inner if statement
            std::cout << x << " is between 0 and 20\n";
        else // attached to inner if statement
            std::cout << x << " is negative\n";
    }

    return 0;
}
```

Copy

This causes the above program to produce incorrect output:

Enter a number: 21
21 is negative


To avoid such ambiguities when nesting `if statements`, it is a good idea to explicitly enclose the inner `if statement` within a block. This allows us to attach an `else` to either `if statement` without ambiguity:

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter a number: ";
    int x{};
    std::cin >> x;

    if (x >= 0)
    {
        if (x <= 20)
            std::cout << x << " is between 0 and 20\n";
        else // attached to inner if statement
            std::cout << x << " is greater than 20\n";
    }
    else // attached to outer if statement
        std::cout << x << " is negative\n";

    return 0;
}
```

Copy

The `else statement` within the block attaches to the inner `if statement`, and the `else statement` outside of the block attaches to the outer `if statement`.




Nested `if statements` can often be flattened by either restructuring the logic or by using logical operators (covered in lesson [6.7 -- Logical operators](https://www.learncpp.com/cpp-tutorial/logical-operators/)). Code that is less nested is less error prone.



Null statements

A **null statement** is an expression statement that consists of just a semicolon:

```cpp
if (x > 10)
    ; // this is a null statement
```

Copy

`Null statements` do nothing. They are typically used when the language requires a statement to exist but the programmer doesn’t need one. For readability, `null statements` are typically placed on their own lines.

We’ll see examples of intentional `null statements` later in this chapter, when we cover loops. `Null statements` are rarely intentionally used with `if statements`. However, they can unintentionally cause problems for new (or careless) programmers. Consider the following snippet:

```cpp
if (nuclearCodesActivated());
    blowUpTheWorld();
```

Copy

In the above snippet, the programmer accidentally put a semicolon on the end of the `if statement` (a common mistake since semicolons end many statements). This unassuming error compiles fine, and causes the snippet to execute as if it had been written like this:

```cpp
if (nuclearCodesActivated())
    ; // the semicolon acts as a null statement
blowUpTheWorld(); // and this line always gets executed!
```



Warning

Be careful not to “terminate” your `if statement` with a semicolon, otherwise your conditional statement(s) will execute unconditionally (even if they are inside a block).



