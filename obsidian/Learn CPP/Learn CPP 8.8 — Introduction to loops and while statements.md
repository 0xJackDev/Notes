

Introduction to loops

And now the real fun begins -- in the next set of lessons, we’ll cover loops. Loops are control flow constructs that allow a piece of code to execute repeatedly until some condition is met. Loops add a significant amount of flexibility into your programming toolkit, allowing you to do many things that would otherwise be difficult.


Intentional infinite loops

We can declare an intentional infinite loop like this:

```cpp
while (true)
{
  // this loop will execute forever
}
```

Copy

The only way to exit an infinite loop is through a return-statement, a break-statement, an exit-statement, a goto-statement, an exception being thrown, or the user killing the program.

Here’s a silly example demonstrating this:

```cpp
#include <iostream>

int main()
{

    while (true) // infinite loop
    {
        std::cout << "Loop again (y/n)? ";
        char c{};
        std::cin >> c;

        if (c == 'n')
            return 0;
    }

    return 0;
}
```

Copy

This program will continuously loop until the user enters `n` as input, at which point the if-statement will evaluate to `true` and the associated `return 0;` will cause function `main()` to exit, terminating the program.

It is common to see this kind of loop in web server applications that run continuously and service web requests.


also in video games with the 'game loop'



Loop variables and naming

A **loop variable** is a variable that is used to control how many times a loop executes. For example, given `while (count <= 10)`, `count` is a loop variable. While most loop variables have type `int`, you will occasionally see other types (e.g. `char`).

Loop variables are often given simple names, with `i`, `j`, and `k` being the most common.

As an aside…

The use of `i`, `j`, and `k` for loop variable names arose because these are the first three shortest names for integral variables in the Fortran programming language. The convention has persisted since.

However, if you want to know where in your program a loop variable is used, and you use the search function on `i`, `j`, or `k`, the search function will return half of the lines in your program! For this reason, some developers prefer loop variable names like `iii`, `jjj`, or `kkk`. Because these names are more unique, this makes searching for loop variables much easier, and helps them stand out as loop variables. An even better idea is to use “real” variable names, such as `count`, `index`, or a name that gives more detail about what you’re counting (e.g. `userCount`).

The most common type of loop variable is called a **counter**, which is a loop variable that counts how many times a loop has executed. In the examples above, the variable `count` is a counter.



