

A **default argument** is a default value provided for a function parameter. For example:

```cpp
void print(int x, int y=10) // 10 is the default argument
{
    std::cout << "x: " << x << '\n';
    std::cout << "y: " << y << '\n';
}
```

Copy

When making a function call, the caller can optionally provide an argument for any function parameter that has a default argument. If the caller provides an argument, the value of the argument in the function call is used. If the caller does not provide an argument, the value of the default argument is used.

Consider the following program:

```cpp
#include <iostream>

void print(int x, int y=4) // 4 is the default argument
{
    std::cout << "x: " << x << '\n';
    std::cout << "y: " << y << '\n';
}

int main()
{
    print(1, 2); // y will use user-supplied argument 2
    print(3); // y will use default argument 4, as if we had called print(3, 4)

    return 0;
}
```

Copy

This program produces the following output:

x: 1
y: 2
x: 3
y: 4

In the first function call, the caller supplied explicit arguments for both parameters, so those argument values are used. In the second function call, the caller omitted the second argument, so the default value of `4` was used.

Note that you must use the equals sign to specify a default argument. Using parenthesis or brace initialization won’t work:

```cpp
void foo(int x = 5);   // ok
void goo(int x ( 5 )); // compile error
void boo(int x { 5 }); // compile error
```

Copy

Perhaps surprisingly, default arguments are handled by the compiler at the call site. In the above example, when the compiler sees `print(3)`, it will rewrite this function call as `print(3, 4)`, so that the number of arguments matches the number of parameters. The rewritten function call then works as per usual.

Key insight

Default arguments are inserted by the compiler at site of the function call.

When to use default arguments

Default arguments are an excellent option when a function needs a value that has a reasonable default value, but for which you want to let the caller override if they wish.

For example, here are a couple of function prototypes for which default arguments might be commonly used:

```cpp
int rollDie(int sides=6);
void openLogFile(std::string filename="default.log");
```



Multiple default arguments

A function can have multiple parameters with default arguments:

```cpp
#include <iostream>

void print(int x=10, int y=20, int z=30)
{
    std::cout << "Values: " << x << " " << y << " " << z << '\n';
}

int main()
{
    print(1, 2, 3); // all explicit arguments
    print(1, 2); // rightmost argument defaulted
    print(1); // two rightmost arguments defaulted
    print(); // all arguments defaulted

    return 0;
}
```

Copy

The following output is produced:

Values: 1 2 3
Values: 1 2 30
Values: 1 20 30
Values: 10 20 30

C++ does not (as of C++23) support a function call syntax such as `print(,,3)` (as a way to provide an explicit value for `z` while using the default arguments for `x` and `y`. This has three major consequences:

1. In a function call, any explicitly provided arguments must be the leftmost arguments (arguments with defaults cannot be skipped).

For example:

```cpp
void print(std::string_view sv="Hello", double d=10.0);

int main()
{
    print();           // okay: both arguments defaulted
    print("Macaroni"); // okay: d defaults to 10.0
    print(20.0);       // error: does not match above function (cannot skip argument for sv)

    return 0;
}
```

Copy

2. If a parameter is given a default argument, all subsequent parameters (to the right) must also be given default arguments.

The following is not allowed:

```cpp
void print(int x=10, int y); // not allowed
```

Copy

Rule

If a parameter is given a default argument, all subsequent parameters (to the right) must also be given default arguments.

3. If more than one parameter has a default argument, the leftmost parameter should be the one most likely to be explicitly set by the user.

Default arguments can not be redeclared, and must be declared before use

Once declared, a default argument can not be redeclared in the same translation unit. That means for a function with a forward declaration and a function definition, the default argument can be declared in either the forward declaration or the function definition, but not both.

```cpp
#include <iostream>

void print(int x, int y=4); // forward declaration

void print(int x, int y=4) // compile error: redefinition of default argument
{
    std::cout << "x: " << x << '\n';
    std::cout << "y: " << y << '\n';
}
```

Copy

The default argument must also be declared in the translation unit before it can be used:

```cpp
#include <iostream>

void print(int x, int y); // forward declaration, no default argument

int main()
{
    print(3); // compile error: default argument for y hasn't been defined yet

    return 0;
}

void print(int x, int y=4)
{
    std::cout << "x: " << x << '\n';
    std::cout << "y: " << y << '\n';
}
```

Copy

The best practice is to declare the default argument in the forward declaration and not in the function definition, as the forward declaration is more likely to be seen by other files and included before use (particularly if it’s in a header file).


Default arguments and function overloading

Functions with default arguments may be overloaded. For example, the following is allowed:

```cpp
#include <iostream>
#include <string_view>

void print(std::string_view s)
{
    std::cout << s << '\n';
}

void print(char c = ' ')
{
    std::cout << c << '\n';
}

int main()
{
    print("Hello, world"); // resolves to print(std::string_view)
    print('a');            // resolves to print(char)
    print();               // resolves to print(char)

    return 0;
}
```

Copy

The function call to `print()` acts as if the user had explicitly called `print(' ')`, which resolves to `print(char)`.

Now consider this case:

```cpp
void print(int x);                  // signature print(int)
void print(int x, int y = 10);      // signature print(int, int)
void print(int x, double y = 20.5); // signature print(int, double)
```

Copy

Default values are not part of a function’s signature, so the above functions are differentiated overloads. Thus the above will compile.

