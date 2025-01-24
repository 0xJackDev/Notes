

Although it is possible to chain many if-else statements together, this is both difficult to read and inefficient. which leads us to switch case statements


Because testing a variable or expression for equality against a set of different values is common, C++ provides an alternative conditional statement called a **switch statement** that is specialized for this purpose. Here is the same program as above using a switch:

```cpp
#include <iostream>

void printDigitName(int x)
{
    switch (x)
    {
    case 1:
        std::cout << "One";
        return;
    case 2:
        std::cout << "Two";
        return;
    case 3:
        std::cout << "Three";
        return;
    default:
        std::cout << "Unknown";
        return;
    }
}

int main()
{
    printDigitName(2);
    std::cout << '\n';

    return 0;
}
```

this is telling the compiler that here if the variable x in this case if the case == 1 then output one.  If two output 2 if 3 output 3 but if it isnt any of those numbers then it will result to the default case which will output unknown.


The idea behind a **switch statement** is simple: an expression (sometimes called the `condition`) is evaluated to produce a value. If the expression’s value is equal to the value after any of the `case labels`, the statements after the matching `case label` are executed. If no matching value can be found and a `default label` exists, the statements after the `default label` are executed instead.


the return portion is a flow control mechanism that tells the compiler hey once this piece of code is ran RETURN the runtime to the Function caller so once one case is found it wont keep running down and trigger all the cases instead it will return the Runtime back to the function caller. 


Starting a switch

We start a `switch statement` by using the `switch` keyword, followed by parentheses with the conditional expression that we would like to evaluate inside. Often the expression is just a single variable, but it can be any valid expression.

The one restriction is that the condition must evaluate to an integral type (see lesson [4.1 -- Introduction to fundamental data types](https://www.learncpp.com/cpp-tutorial/introduction-to-fundamental-data-types/) if you need a reminder which fundamental types are considered integral types) or an enumerated type (covered in future lesson [13.2 -- Unscoped enumerations](https://www.learncpp.com/cpp-tutorial/unscoped-enumerations/)), or be convertible to one. Expressions that evaluate to floating point types, strings, and most other non-integral types may not be used here.




Case labels

The first kind of label is the **case label**, which is declared using the `case` keyword and followed by a constant expression. The constant expression must either match the type of the condition or must be convertible to that type.

If the value of the conditional expression equals the expression after a `case label`, execution begins at the first statement after that `case label` and then continues sequentially.



No matching case label and no default case

If the value of the conditional expression does not match any of the case labels, and no default case has been provided, then no cases inside the switch are executed. Execution continues after the end of the switch block.

```cpp
#include <iostream>

void printDigitName(int x)
{
    switch (x) // x is evaluated to produce value 5
    {
    case 1:
        std::cout << "One";
        return;
    case 2:
        std::cout << "Two";
        return;
    case 3:
        std::cout << "Three";
        return;
    // no matching case exists and there is no default case
    }

    // so execution continues here
    std::cout << "Hello";
}

int main()
{
    printDigitName(5);
    std::cout << '\n';

    return 0;
}
```

Copy

In the above example, `x` evalutes to `5`, but there is no case label matching `5`, nor is there a default case. As a result, no cases execute. Execution continues after the switch block, printing `Hello`.



Taking a break

In the above examples, we used `return statements` to stop execution of the statements after our labels. However, this also exits the entire function.

A **break statement** (declared using the `break` keyword) tells the compiler that we are done executing statements within the switch, and that execution should continue with the statement after the end of the switch block. This allows us to exit a `switch statement` without exiting the entire function.

Here’s a slightly modified example rewritten using `break` instead of `return`:

```cpp
#include <iostream>

void printDigitName(int x)
{
    switch (x) // x evaluates to 3
    {
    case 1:
        std::cout << "One";
        break;
    case 2:
        std::cout << "Two";
        break;
    case 3:
        std::cout << "Three"; // execution starts here
        break; // jump to the end of the switch block
    default:
        std::cout << "Unknown";
        break;
    }

    // execution continues here
    std::cout << " Ah-Ah-Ah!";
}

int main()
{
    printDigitName(3);
    std::cout << '\n';

    return 0;
}
```

Copy

The above example prints:

Three Ah-Ah-Ah!



Each set of statements underneath a label should end in a `break statement` or a `return statement`. This includes the statements underneath the last label in the switch.



