

There’s a subtle redundancy lurking in this simple variable definition:

```cpp
double d{ 5.0 };
```

Copy

In C++, we are required to provide an explicit type for all objects. Thus, we’ve specified that variable `d` is of type double.

However, the literal value `5.0` used to initialize `d` also has type double (implicitly determined via the format of the literal).

Related content

We discuss how literal types are determined in lesson [5.2 -- Literals](https://www.learncpp.com/cpp-tutorial/literals/).

In cases where we want a variable and its initializer to have the same type, we’re effectively providing the same type information twice.


Type deduction for initialized variables

**Type deduction** (also sometimes called **type inference**) is a feature that allows the compiler to deduce the type of an object from the object’s initializer. To use type deduction with variables, the `auto` keyword is used in place of the variable’s type:

```cpp
int main()
{
    auto d{ 5.0 }; // 5.0 is a double literal, so d will be type double
    auto i{ 1 + 2 }; // 1 + 2 evaluates to an int, so i will be type int
    auto x { i }; // i is an int, so x will be type int too

    return 0;
}
```

Copy

In the first case, because `5.0` is a double literal, the compiler will deduce that variable `d` should be of type `double`. In the second case, the expression `1 + 2` yields an int result, so variable `i` will be of type `int`. In the third case, `i` was previously deduced to be of type `int`, so `x` will also be deduced to be of type `int`.


This seems kinda useless only to help devs type less but like u still have to type auto so...


DONT USE auto keyword with C style strings



If you wanna use auto make sure your using std::string or std::string view.


