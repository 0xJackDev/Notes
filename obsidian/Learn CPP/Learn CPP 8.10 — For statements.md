

The for-statement looks pretty simple in abstract:

for (init-statement; condition; end-expression)
   statement;


Evaluation of for-statements

A for-statement is evaluated in 3 parts:

First, the init-statement is executed. This only happens once when the loop is initiated. The init-statement is typically used for variable definition and initialization. These variables have “loop scope”, which really just is a form of block scope where these variables exist from the point of definition through the end of the loop statement. In our while-loop equivalent, you can see that the init-statement is inside a block that contains the loop, so the variables defined in the init-statement go out of scope when the block containing the loop ends.

Second, with each loop iteration, the condition is evaluated. If this evaluates to `true`, the statement is executed. If this evaluates to `false`, the loop terminates and execution continues with the next statement beyond the loop.

Finally, after the statement is executed, the end-expression is evaluated. Typically, this expression is used to increment or decrement the loop variables defined in the init-statement. After the end-expression has been evaluated, execution returns to the second step (and the condition is evaluated again).



Off-by-one errors

One of the biggest problems that new programmers have with for-loops (and other loops that utilize counters) are off-by-one errors. **Off-by-one errors** occur when the loop iterates one too many or one too few times to produce the desired result.

Here’s an example:

```cpp
#include <iostream>

int main()
{
    // oops, we used operator< instead of operator<=
    for (int i{ 1 }; i < 5; ++i)
    {
        std::cout << i << ' ';
    }

    std::cout << '\n';

    return 0;
}
```

Copy

This program is supposed to print `1 2 3 4 5`, but it only prints `1 2 3 4` because we used the wrong relational operator.

Although the most common cause for these errors is using the wrong relational operator, they can sometimes occur by using pre-increment or pre-decrement instead of post-increment or post-decrement, or vice-versa.



Omitted expressions

It is possible to write _for loops_ that omit any or all of the statements or expressions. For example, in the following example, we’ll omit the init-statement and end-expression, leaving only the condition:

```cpp
#include <iostream>

int main()
{
    int i{ 0 };
    for ( ; i < 10; ) // no init-statement or end-expression
    {
        std::cout << i << ' ';
        ++i;
    }

    std::cout << '\n';

    return 0;
}
```

Copy

This _for loop_ produces the result:

0 1 2 3 4 5 6 7 8 9

Rather than having the _for loop_ do the initialization and incrementing, we’ve done it manually. We have done so purely for academic purposes in this example, but there are cases where not defining a loop variable (because you already have one) or not incrementing it in the end-expression (because you’re incrementing it some other way) is desired.




For-loops with multiple counters

Although for-loops typically iterate over only one variable, sometimes for-loops need to work with multiple variables. To assist with this, the programmer can define multiple variables in the init-statement, and can make use of the comma operator to change the value of multiple variables in the end-expression:

```cpp
#include <iostream>

int main()
{
    for (int x{ 0 }, y{ 9 }; x < 10; ++x, --y)
        std::cout << x << ' ' << y << '\n';

    return 0;
}
```

Copy

This loop defines and initializes two new variables: `x` and `y`. It iterates `x` over the range `0` to `9`, and after each iteration `x` is incremented and `y` is decremented.

Nested for-loops

Like other types of loops, for-loops can be nested inside other loops. In the following example, we’re nesting a for-loop inside another for-loop:

```cpp
#include <iostream>

int main()
{
	for (char c{ 'a' }; c <= 'e'; ++c) // outer loop on letters
	{
		std::cout << c; // print our letter first

		for (int i{ 0 }; i < 3; ++i) // inner loop on all numbers
			std::cout << i;

		std::cout << '\n';
	}

	return 0;
}
```

Copy

For each iteration of the outer loop, the inner loop runs in its entirety. Consequently, the output is:

a012
b012
c012
d012
e012

Here’s some more detail on what’s happening here. The outer loop runs first, and char `c` is initialized to `'a'`. Then `c <= 'e'` is evaluated, which is `true`, so the loop body executes. Since `c` is set to `'a'`, this first prints `a`. Next the inner loop executes entirely (which prints `0`, `1`, and `2`). Then a newline is printed. Now the outer loop body is finished, so the outer loop returns to the top, `c` is incremented to `'b'`, and the loop condition is re-evaluated. Since the loop condition is still `true` the next iteration of the outer loop begins. This prints `b012\n`. And so on.




Variables used only inside a loop should be defined inside the loop


Conclusion

For-statements are the most commonly used loop in the C++ language. Even though its syntax is typically a bit confusing to new programmers, you will see for-loops so often that you will understand them in no time at all!

For-statements excel when you have a counter variable. If you do not have a counter, a while-statement is probably a better choice.


