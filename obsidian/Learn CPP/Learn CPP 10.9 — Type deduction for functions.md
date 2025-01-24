
Consider the following program:

```cpp
int add(int x, int y)
{
    return x + y;
}
```

Copy

When this function is compiled, the compiler will determine that `x + y` evaluates to an `int`, then ensure that type of the return value matches the declared return type of the function (or that the return value type can be converted to the declared return type).

Since the compiler already has to deduce the return type from the return statement, in C++14, the `auto` keyword was extended to do function return type deduction. This works by using the `auto` keyword in place of the function’s return type.

For example:

```cpp
auto add(int x, int y)
{
    return x + y;
}
```

Copy

Because the return statement is returning an `int` value, the compiler will deduce that the return type of this function is `int`.

When using an `auto` return type, all return statements within the function must return values of the same type, otherwise an error will result. For example:

```cpp
auto someFcn(bool b)
{
    if (b)
        return 5; // return type int
    else
        return 6.7; // return type double
}
```

Copy

In the above function, the two return statements return values of different types, so the compiler will give an error.

If such a case is desired for some reason, you can either explicitly specify a return type for your function (in which case the compiler will try to implicitly convert any non-matching return expressions to the explicit return type), or you can explicitly convert all of your return statements to the same type. In the example above, the latter could be done by changing `5` to `5.0`, but `static_cast` can also be used for non-literal types.

A major downside of functions that use an `auto` return type is that such functions must be fully defined before they can be used (a forward declaration is not sufficient). For example:



A major downside of functions that use an `auto` return type is that such functions must be fully defined before they can be used (a forward declaration is not sufficient). For example:


Best practice

Favor explicit return types over function return type deduction for normal functions.



