

While relational (comparison) operators can be used to test whether a particular condition is true or false, they can only test one condition at a time. Often we need to know whether multiple conditions are true simultaneously. For example, to check whether we’ve won the lottery, we have to compare whether all of the multiple numbers we picked match the winning numbers. In a lottery with 6 numbers, this would involve 6 comparisons, _all_ of which have to be true. In other cases, we need to know whether any one of multiple conditions is true. For example, we may decide to skip work today if we’re sick, or if we’re too tired, or if we won the lottery in our previous example. This would involve checking whether _any_ of 3 comparisons is true.

Logical operators provide us with the capability to test multiple conditions.

C++ has 3 logical operators:

|Operator|Symbol|Example Usage|Operation|
|---|---|---|---|
|Logical NOT|!|!x|true if x is false, or false if x is true|
|Logical AND|&&|x && y|true if x and y are both true, false otherwise|
|Logical OR|\||x \| y|true if either (or both) x or y are true, false otherwise|
You have already run across the logical NOT unary operator in lesson [4.9 -- Boolean values](https://www.learncpp.com/cpp-tutorial/boolean-values/). We can summarize the effects of logical NOT like so:

|Logical NOT (operator !)|   |
|---|---|
|Operand|Result|
|true|false|
|false|true|

If _logical NOT’s_ operand evaluates to true, _logical NOT_ evaluates to false. If _logical NOT’s_ operand evaluates to false, _logical NOT_ evaluates to true. In other words, _logical NOT_ flips a Boolean value from true to false, and vice-versa.

Logical NOT is often used in conditionals:

```cpp
bool tooLarge { x > 100 }; // tooLarge is true if x > 100
if (!tooLarge)
    // do something with x
else
    // print an error
```

Copy

One thing to be wary of is that _logical NOT_ has a very high level of precedence. New programmers often make the following mistake:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int y{ 7 };

    if (!x > y)
        std::cout << x << " is not greater than " << y << '\n';
    else
        std::cout << x << " is greater than " << y << '\n';

    return 0;
}
```

Copy

This program prints:

5 is greater than 7

But _x_ is not greater than _y_, so how is this possible? The answer is that because the _logical NOT_ operator has higher precedence than the _greater than_ operator, the expression `! x > y` actually evaluates as `(!x) > y`. Since _x_ is 5, !x evaluates to _0_, and `0 > y` is false, so the _else_ statement executes!

The correct way to write the above snippet is:

```cpp
#include <iostream>

int main()
{
    int x{ 5 };
    int y{ 7 };

    if (!(x > y))
        std::cout << x << " is not greater than " << y << '\n';
    else
        std::cout << x << " is greater than " << y << '\n';

    return 0;
}
```

Copy

This way, `x > y` will be evaluated first, and then logical NOT will flip the Boolean result.



## Logical OR

The _logical OR_ operator is used to test whether either of two conditions is true. If the left operand evaluates to true, or the right operand evaluates to true, or both are true, then the _logical OR_ operator returns true. Otherwise it will return false.




## Logical AND

The _logical AND_ operator is used to test whether both operands are true. If both operands are true, _logical AND_ returns true. Otherwise, it returns false.


Short circuit evaluation

In order for _logical AND_ to return true, both operands must evaluate to true. If the left operand evaluates to false, _logical AND_ knows it must return false regardless of whether the right operand evaluates to true or false. In this case, the _logical AND_ operator will go ahead and return false immediately without even evaluating the right operand! This is known as **short circuit evaluation**, and it is done primarily for optimization purposes.



## Mixing ANDs and ORs

Mixing _logical AND_ and _logical OR_ operators in the same expression often can not be avoided, but it is an area full of potential dangers.

Because _logical AND_ and _logical OR_ seem like a pair, many programmers assume they have the same precedence (just like addition/subtraction and multiplication/division). However, _logical AND_ has higher precedence than _logical OR_, thus _logical AND_ operators will be evaluated ahead of _logical OR_ operators (unless they have been parenthesized).

New programmers will often write expressions such as `value1 || value2 && value3`. Because _logical AND_ has higher precedence, this evaluates as `value1 || (value2 && value3)`, not `(value1 || value2) && value3`. Hopefully that’s what the programmer wanted! If the programmer was assuming left to right association (as happens with addition/subtraction, or multiplication/division), the programmer will get a result he or she was not expecting!

When mixing _logical AND_ and _logical OR_ in the same expression, it is a good idea to explicitly parenthesize each operator and its operands. This helps prevent precedence mistakes, makes your code easier to read, and clearly defines how you intended the expression to evaluate. For example, rather than writing `value1 && value2 || value3 && value4`, it is better to write `(value1 && value2) || (value3 && value4)`.

Best practice

When mixing _logical AND_ and _logical OR_ in a single expression, explicitly parenthesize each operation to ensure they evaluate how you intend.


De Morgan’s laws

Many programmers also make the mistake of thinking that `!(x && y)` is the same thing as `!x && !y`. Unfortunately, you can not “distribute” the _logical NOT_ in that manner.

[De Morgan’s laws](https://en.wikipedia.org/wiki/De_Morgan%27s_laws) tell us how the _logical NOT_ should be distributed in these cases:

`!(x && y)` is equivalent to `!x || !y`  
`!(x || y)` is equivalent to `!x && !y`

In other words, when you distribute the _logical NOT_, you also need to flip _logical AND_ to _logical OR_, and vice-versa!

This can sometimes be useful when trying to make complex expressions easier to read.





## Where’s the logical exclusive or (XOR) operator?

_Logical XOR_ is a logical operator provided in some languages that is used to test whether an odd number of conditions is true:

|Logical XOR|   |   |
|---|---|---|
|Left operand|Right operand|Result|
|false|false|false|
|false|true|true|
|true|false|true|
|true|true|false|

C++ doesn’t provide an explicit _logical XOR_ operator (`operator^` is a bitwise XOR, not a logical XOR). Unlike _logical OR_ or _logical AND_, _logical XOR_ cannot be short circuit evaluated. Because of this, making a _logical XOR_ operator out of _logical OR_ and _logical AND_ operators is challenging.

However, `operator!=` produces the same result as a logical XOR when given `bool` operands:

|Left operand|Right operand|logical XOR|operator!=|
|---|---|---|---|
|false|false|false|false|
|false|true|true|true|
|true|false|true|true|
|true|true|false|false|

Therefore, a logical XOR can be implemented as follows:

```cpp
if (a != b) ... // a XOR b, assuming a and b are bool
```

Copy

This can be extended to multiple operands as follows:

```cpp
if (a != b != c) ... // a XOR b XOR c, assuming a, b, and c are bool
```

Copy

If the operands are not of type `bool`, using `operator!=` to implement a logical XOR will not work as expected.



