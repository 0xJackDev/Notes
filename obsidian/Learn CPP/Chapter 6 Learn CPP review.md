Quick review

Always use parentheses to disambiguate the precedence of operators if there is any question or opportunity for confusion.

The arithmetic operators all work like they do in normal mathematics. The remainder (%) operator returns the remainder from an integer division.

The increment and decrement operators can be used to easily increment or decrement numbers. Avoid the postfix versions of these operators whenever possible.

Beware of side effects, particularly when it comes to the order that function parameters are evaluated. Do not use a variable that has a side effect applied more than once in a given statement.

The comma operator can compress multiple statements into one. Writing the statements separately is usually better.

The conditional operator is a nice short version of an if-statement, but don’t use it as an alternative to an if-statement. Only use the conditional operator if you use its result.

Relational operators can be used to compare floating point numbers. Beware using equality and inequality on floating point numbers.

Logical operators allow us to form compound conditional statements.


Why should you never do the following:

a) int y{ foo(++x, x) };

Hide Solution

Because operator++ applies a side effect to x, we should not use x again in the same expression. In this case, the parameters to function foo() can be evaluated in any order, so it’s indeterminate whether x or ++x gets evaluated first. Because ++x changes the value of x, it’s unclear what values will be passed into the function.