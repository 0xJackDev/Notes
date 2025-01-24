

Incrementing and decrementing variables

Incrementing (adding 1 to) and decrementing (subtracting 1 from) a variable are both so common that they have their own operators.

|Operator|Symbol|Form|Operation|
|---|---|---|---|
|Prefix increment (pre-increment)|++|++x|Increment x, then return x|
|Prefix decrement (pre-decrement)|––|––x|Decrement x, then return x|
|Postfix increment (post-increment)|++|x++|Copy x, then increment x, then return the copy|
|Postfix decrement (post-decrement)|––|x––|Copy x, then decrement x, then return the copy|

Note that there are two versions of each operator -- a prefix version (where the operator comes before the operand) and a postfix version (where the operator comes after the operand).



Prefix increment and decrement

The prefix increment/decrement operators are very straightforward. First, the operand is incremented or decremented, and then expression evaluates to the value of the operand. For example:

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    int y { ++x }; // x is incremented to 6, x is evaluated to the value 6, and 6 is assigned to y

    std::cout << x << ' ' << y << '\n';
    return 0;
}
```

Copy

This prints:

6 6



Postfix increment and decrement

The postfix increment/decrement operators are trickier. First, a copy of the operand is made. Then the operand (not the copy) is incremented or decremented. Finally, the copy (not the original) is evaluated. For example:

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    int y { x++ }; // x is incremented to 6, copy of original x is evaluated to the value 5, and 5 is assigned to y

    std::cout << x << ' ' << y << '\n';
    return 0;
}
```

Copy

This prints:

6 5

Let’s examine how this line 6 works in more detail. First, a temporary copy of _x_ is made that starts with the same value as _x_ (5). Then the actual _x_ is incremented from _5_ to _6_. Then the copy of _x_ (which still has value _5_) is returned and assigned to _y_. Then the temporary copy is discarded.

Consequently, _y_ ends up with the value of _5_ (the pre-incremented value), and _x_ ends up with the value _6_ (the post-incremented value).

Note that the postfix version takes a lot more steps, and thus may not be as performant as the prefix version.


Best practice

Favor the prefix versions, as they are more performant and less likely to cause surprises.


Side effects

A function or expression is said to have a **side effect** if it has some observable effect beyond producing a return value.

Common examples of side effects include changing the value of objects, doing input or output, or updating a graphical user interface (e.g. enabling or disabling a button).

Most of the time, side effects are useful:

```cpp
x = 5; // the assignment operator has side effect of changing value of x
++x; // operator++ has side effect of incrementing x
std::cout << x; // operator<< has side effect of modifying the state of the console
```

Copy

The assignment operator in the above example has the side effect of changing the value of _x_ permanently. Even after the statement has finished executing, _x_ will still have the value 5. Similarly with operator++, the value of _x_ is altered even after the statement has finished evaluating. The outputting of _x_ also has the side effect of modifying the state of the console, as you can now see the value of _x_ printed to the console.


Side effects can cause order of evaluation issues

In some cases, side effects can lead to order of evaluation problems. For example:

```cpp
#include <iostream>

int add(int x, int y)
{
    return x + y;
}

int main()
{
    int x { 5 };
    int value{ add(x, ++x) }; // undefined behavior: is this 5 + 6, or 6 + 6?
    // It depends on what order your compiler evaluates the function arguments in

    std::cout << value << '\n'; // value could be 11 or 12, depending on how the above line evaluates!

    return 0;
}
```

Copy

The C++ standard does not define the order in which function arguments are evaluated. If the left argument is evaluated first, this becomes a call to add(5, 6), which equals 11. If the right argument is evaluated first, this becomes a call to add(6, 6), which equals 12! Note that this is only a problem because one of the arguments to function add() has a side effect.



