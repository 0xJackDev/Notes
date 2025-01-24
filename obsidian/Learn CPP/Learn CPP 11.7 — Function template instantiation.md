
In the previous lesson ([11.6 -- Function templates](https://www.learncpp.com/cpp-tutorial/function-templates/)), we introduced function templates, and converted a normal `max()` function into a `max<T>` function template:

```cpp
template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}
```

Copy

In this lesson, we’ll focus on how function templates are used.

Using a function template

Function templates are not actually functions -- their code isn’t compiled or executed directly. Instead, function templates have one job: to generate functions (that are compiled and executed).

To use our `max<T>` function template, we can make a function call with the following syntax:

max<actual_type>(arg1, arg2); // actual_type is some actual type, like int or double

This looks a lot like a normal function call -- the primary difference is the addition of the type in angled brackets (called a **template argument**), which specifies the actual type that will be used in place of template type `T`.

Let’s take a look at this in a simple example:

```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max<int>(1, 2) << '\n'; // instantiates and calls function max<int>(int, int)

    return 0;
}
```

Copy

When the compiler encounters the function call `max<int>(1, 2)`, it will determine that a function definition for `max<int>(int, int)` does not already exist. Consequently, the compiler will implicitly use our `max<T>` function template to create one.

The process of creating functions (with specific types) from function templates (with template types) is called **function template instantiation** (or **instantiation** for short). When a function is instantiated due to a function call, it’s called **implicit instantiation**. A function that is instantiated from a template is technically called a **specialization**, but in common language is often called a **function instance**. The template from which a specialization is produced is called a **primary template**. Function instances are normal functions in all regards.


The process for instantiating a function is simple: the compiler essentially clones the primary template and replaces the template type (`T`) with the actual type we’ve specified (`int`).

So when we call `max<int>(1, 2)`, the function specialization that gets instantiated looks something like this:

```cpp
template<> // ignore this for now
int max<int>(int x, int y) // the generated function max<int>(int, int)
{
    return (x < y) ? y : x;
}
```

Copy

Here’s the same example as above, showing what the compiler actually compiles after all instantiations are done:

```cpp
#include <iostream>

// a declaration for our function template (we don't need the definition any more)
template <typename T>
T max(T x, T y);

template<>
int max<int>(int x, int y) // the generated function max<int>(int, int)
{
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max<int>(1, 2) << '\n'; // instantiates and calls function max<int>(int, int)

    return 0;
}
```

Copy

You can compile this yourself and see that it works. A function template is only instantiated the first time a function call is made in each translation unit. Further calls to the function are routed to the already instantiated function.

Conversely, if no function call is made to a function template, the function template won’t be instantiated in that translation unit.



Template argument deduction

In most cases, the actual types we want to use for instantiation will match the type of our function parameters. For example:

```cpp
std::cout << max<int>(1, 2) << '\n'; // specifying we want to call max<int>
```

Copy

In this function call, we’ve specified that we want to replace `T` with `int`, but we’re also calling the function with `int` arguments.

In cases where the type of the arguments match the actual type we want, we do not need to specify the actual type -- instead, we can use **template argument deduction** to have the compiler deduce the actual type that should be used from the argument types in the function call.

For example, instead of making a function call like this:

```cpp
std::cout << max<int>(1, 2) << '\n'; // specifying we want to call max<int>
```

Copy

We can do one of these instead:

```cpp
std::cout << max<>(1, 2) << '\n';
std::cout << max(1, 2) << '\n';
```

Copy

In either case, the compiler will see that we haven’t provided an actual type, so it will attempt to deduce an actual type from the function arguments that will allow it to generate a `max()` function where all template parameters match the type of the provided arguments. In this example, the compiler will deduce that using function template `max<T>` with actual type `int` allows it to instantiate function `max<int>(int, int)`, so that the type of both function parameters (`int`) matches the type of the provided arguments (`int`).

The difference between the two cases has to do with how the compiler resolves the function call from a set of overloaded functions. In the top case (with the empty angled brackets), the compiler will only consider `max<int>` template function overloads when determining which overloaded function to call. In the bottom case (with no angled brackets), the compiler will consider both `max<int>` template function overloads and `max` non-template function overloads. When the bottom case results in both a template function and a non-template function that are equally viable, the non-template function will be preferred.

Key insight

The normal function call syntax will prefer a non-template function over an equally viable function instantiated from a template.

For example:

```cpp
#include <iostream>

template <typename T>
T max(T x, T y)
{
    std::cout << "called max<int>(int, int)\n";
    return (x < y) ? y : x;
}

int max(int x, int y)
{
    std::cout << "called max(int, int)\n";
    return (x < y) ? y : x;
}

int main()
{
    std::cout << max<int>(1, 2) << '\n'; // calls max<int>(int, int)
    std::cout << max<>(1, 2) << '\n';    // deduces max<int>(int, int) (non-template functions not considered)
    std::cout << max(1, 2) << '\n';      // calls max(int, int)

    return 0;
}
```

Copy

Note how the syntax in the bottom case looks identical to a normal function call! In most cases, this normal function call syntax will be the one we use to call functions instantiated from a function template.

There are a few reasons for this:

- The syntax is more concise.
- It’s rare that we’ll have both a matching non-template function and a function template.
- If we do have a matching non-template function and a matching function template, we will usually prefer the non-template function to be called.


Best practice

Favor the normal function call syntax when making calls to a function instantiated from a function template (unless you need the function template version to be preferred over a matching non-template function).


Function templates with non-template parameters

It’s possible to create function templates that have both template parameters and non-template parameters. The type template parameters can be matched to any type, and the non-template parameters work like the parameters of normal functions.

For example:

```cpp
// T is a type template parameter
// double is a non-template parameter
// We don't need to provide names for these parameters since they aren't used
template <typename T>
int someFcn(T, double)
{
    return 5;
}

int main()
{
    someFcn(1, 3.4); // matches someFcn(int, double)
    someFcn(1, 3.4f); // matches someFcn(int, double) -- the float is promoted to a double
    someFcn(1.2, 3.4); // matches someFcn(double, double)
    someFcn(1.2f, 3.4); // matches someFcn(float, double)
    someFcn(1.2f, 3.4f); // matches someFcn(float, double) -- the float is promoted to a double

    return 0;
}
```

Copy

This function template has a templated first parameter, but the second parameter is fixed with type `double`. Note that the return type can also be any type. In this case, our function will always return an `int` value.


Instantiated functions may not always compile

Consider the following program:

```cpp
#include <iostream>

template <typename T>
T addOne(T x)
{
    return x + 1;
}

int main()
{
    std::cout << addOne(1) << '\n';
    std::cout << addOne(2.3) << '\n';

    return 0;
}
```

Copy

The compiler will effectively compile and execute this:

```cpp
#include <iostream>

template <typename T>
T addOne(T x);

template<>
int addOne<int>(int x)
{
    return x + 1;
}

template<>
double addOne<double>(double x)
{
    return x + 1;
}

int main()
{
    std::cout << addOne(1) << '\n';   // calls addOne<int>(int)
    std::cout << addOne(2.3) << '\n'; // calls addOne<double>(double)

    return 0;
}
```

Copy

which will produce the result:

2
3.3

But what if we try something like this?

```cpp
#include <iostream>
#include <string>

template <typename T>
T addOne(T x)
{
    return x + 1;
}

int main()
{
    std::string hello { "Hello, world!" };
    std::cout << addOne(hello) << '\n';

    return 0;
}
```

Copy

When the compiler tries to resolve `addOne(hello)` it won’t find a non-template function match for `addOne(std::string)`, but it will find our function template for `addOne(T)`, and determine that it can generate an `addOne(std::string)` function from it. Thus, the compiler will generate and compile this:

```cpp
#include <iostream>
#include <string>

template <typename T>
T addOne(T x);

template<>
std::string addOne<std::string>(std::string x)
{
    return x + 1;
}

int main()
{
    std::string hello{ "Hello, world!" };
    std::cout << addOne(hello) << '\n';

    return 0;
}
```

Copy

However, this will generate a compile error, because `x + 1` doesn’t make sense when `x` is a `std::string`. The obvious solution here is simply not to call `addOne()` with an argument of type `std::string`.


Instantiated functions may not always make sense semantically

The compiler will successfully compile an instantiated function template as long as it makes sense syntactically. However, the compiler does not have any way to check that such a function actually makes sense semantically.

For example:

```cpp
#include <iostream>

template <typename T>
T addOne(T x)
{
    return x + 1;
}

int main()
{
    std::cout << addOne("Hello, world!") << '\n';

    return 0;
}
```

Copy

In this example, we’re calling `addOne()` on a C-style string literal. What does that actually mean semantically? Who knows!

Perhaps surprisingly, because C++ syntactically allows addition of an integer value to a string literal (we cover this in future lesson [17.9 -- Pointer arithmetic and subscripting](https://www.learncpp.com/cpp-tutorial/pointer-arithmetic-and-subscripting/)), the above example compiles, and produces the following result:

ello, world!

Warning

The compiler will instantiate and compile function templates that do not make sense semantically as long as they are syntactically valid. It is your responsibility to make sure you are calling such function templates with arguments that make sense.


Beware function templates with modifiable static local variables

In lesson [7.10 -- Static local variables](https://www.learncpp.com/cpp-tutorial/static-local-variables/), we discussed static local variables, which are local variables with static duration (they persist for the lifetime of the program).

When a static local variable is used in a function template, each function instantiated from that template will have a separate version of the static local variable. This is rarely a problem if the static local variable is const. But if the static local variable is one that is modified, the results may not be as expected.

For example:

```cpp
#include <iostream>

// Here's a function template with a static local variable that is modified
template <typename T>
void printIDAndValue(T value)
{
    static int id{ 0 };
    std::cout << ++id << ") " << value << '\n';
}

int main()
{
    printIDAndValue(12);
    printIDAndValue(13);

    printIDAndValue(14.5);

    return 0;
}
```

Copy

This produces the result:

1) 12
2) 13
1) 14.5

You may have been expecting the last line to print `3) 14.5`. However, this is what the compiler actually compiles and executes:

```cpp
#include <iostream>

template <typename T>
void printIDAndValue(T value);

template <>
void printIDAndValue<int>(int value)
{
    static int id{ 0 };
    std::cout << ++id << ") " << value << '\n';
}

template <>
void printIDAndValue<double>(double value)
{
    static int id{ 0 };
    std::cout << ++id << ") " << value << '\n';
}

int main()
{
    printIDAndValue(12);   // calls printIDAndValue<int>()
    printIDAndValue(13);   // calls printIDAndValue<int>()

    printIDAndValue(14.5); // calls printIDAndValue<double>()

    return 0;
}
```

Copy

Note that `printIDAndValue<int>` and `printIDAndValue<double>` each have their own independent static local variable named `id`, not one that is shared between them.


Generic programming

Because template types can be replaced with any actual type, template types are sometimes called **generic types**. And because templates can be written agnostically of specific types, programming with templates is sometimes called **generic programming**. Whereas C++ typically has a strong focus on types and type checking, in contrast, generic programming lets us focus on the logic of algorithms and design of data structures without having to worry so much about type information.

Conclusion

Once you get used to writing function templates, you’ll find they actually don’t take much longer to write than functions with actual types. Function templates can significantly reduce code maintenance and errors by minimizing the amount of code that needs to be written and maintained.

Function templates do have a few drawbacks, and we would be remiss not to mention them. First, the compiler will create (and compile) a function for each function call with a unique set of argument types. So while function templates are compact to write, they can expand into a crazy amount of code, which can lead to code bloat and slow compile times. The bigger downside of function templates is that they tend to produce crazy-looking, borderline unreadable error messages that are much harder to decipher than those of regular functions. These error messages can be quite intimidating, but once you understand what they are trying to tell you, the problems they are pinpointing are often quite straightforward to resolve.

These drawbacks are fairly minor compared with the power and safety that templates bring to your programming toolkit, so use templates liberally anywhere you need type flexibility! A good rule of thumb is to create normal functions at first, and then convert them into function templates if you find you need an overload for different parameter types.


