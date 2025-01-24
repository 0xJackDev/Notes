
Having to create overloaded functions with the same implementation for each set of parameter types we want to support is a maintenance headache, a recipe for errors, and a clear violation of the DRY (don’t repeat yourself) principle. There’s a less-obvious challenge here as well: a programmer who wishes to use the `max` function may wish to call it with an argument type that the author of the `max` did not anticipate (and thus did not write an overloaded function for).

What we are really missing is some way to write a single version of `max` that can work with arguments of any type (even types that may not have been anticipated when the code for `max` was written). Normal functions are simply not up to the task here. Fortunately, C++ supports another feature that was designed specifically to solve this kind of problem.

Welcome to the world of C++ templates.

Introduction to C++ templates

In C++, the template system was designed to simplify the process of creating functions (or classes) that are able to work with different data types.

Instead of manually creating a bunch of mostly-identical functions or classes (one for each set of different types), we instead create a single _template_. Just like a normal definition, a **template** describes what a function or class looks like. Unlike a normal definition (where all types must be specified), in a template we can use one or more placeholder types. A placeholder type represents some type that is not known at the time the template is written, but that will be provided later.

Once a template is defined, the compiler can use the template to generate as many overloaded functions (or classes) as needed, each using different actual types!

The end result is the same -- we end up with a bunch of mostly-identical functions or classes (one for each set of different types). But we only have to create and maintain a single template, and the compiler does all the hard work for us.

Key insight

The compiler can use a single template to generate a family of related functions or classes, each using a different set of types.



Because the actual types aren’t determined until the template is used in a program (not when the template is written), the author of the template doesn’t have to try to anticipate all of the actual types that might be used. This means template code can be used with types that didn’t even exist when the template was written! We’ll see how this comes in handy later, when we start exploring the C++ standard library, which is absolutely full of template code!


Function templates

A **function template** is a function-like definition that is used to generate one or more overloaded functions, each with a different set of actual types. This is what will allow us to create functions that can work with many different types.

When we create our function template, we use placeholder types (also called **type template parameters**, or informally **template types**) for any parameter types, return types, or types used in the function body that we want to be specified later.

For advanced readers

C++ supports 3 different kinds of template parameters:

- Type template parameters (where the template parameter represents a type).
- Non-type template parameters (where the template parameter represents a constexpr value).
- Template template parameters (where the template parameter represents a template).

Type template parameters are by far the most common, so we’ll be focused on those. We’ll cover non-type template parameters in the chapter on arrays.

Function templates are something that is best taught by example, so let’s convert our normal `max(int, int)` function from the example above into a function template. It’s surprisingly easy, and we’ll explain what’s happening along the way.

Creating a templated max function

Here’s the int version of `max` again:

```cpp
int max(int x, int y)
{
    return (x < y) ? y : x;
}
```

Copy

Note that we use type `int` three times in this function: once for parameter `x`, once for parameter `y`, and once for the return type of the function.

To create a function template, we’re going to do two things. First, we’re going to replace our specific types with type template parameters. In this case, because we have only one type that needs replacing (`int`), we only need one type template parameter (which we’ll call `T`):

Here’s our new function that uses a single template type:

```cpp
T max(T x, T y) // won't compile because we haven't defined T
{
    return (x < y) ? y : x;
}
```

Copy

This is a good start -- however, it won’t compile because the compiler doesn’t know what `T` is! And this is still a normal function, not a function template.

Second, we’re going to tell the compiler that this is a function template, and that `T` is a type template parameter that is a placeholder for any type. This is done using what is called a **template parameter declaration**. The scope of a template parameter declaration is limited to the function template (or class template) that follows. Therefore, each function template (or class) needs its own template parameter declaration.

```cpp
template <typename T> // this is the template parameter declaration
T max(T x, T y) // this is the function template definition for max<T>
{
    return (x < y) ? y : x;
}
```

Copy

In our template parameter declaration, we start with the keyword `template`, which tells the compiler that we’re creating a template. Next, we specify all of the template parameters that our template will use inside angled brackets (`<>`). For each type template parameter, we use the keyword `typename` or `class`, followed by the name of the type template parameter (e.g. `T`).


As an aside…

There is no difference between the `typename` and `class` keywords in this context. You will often see people use the `class` keyword since it was introduced into the language earlier. However, we prefer the newer `typename` keyword, because it makes it clearer that the type template parameter can be replaced by any type (such as a fundamental type), not just class types.



Believe it or not, we’re done! We have created a template version of our `max` function that can now accept arguments of different types.

Because this function template has one template type named `T`, we’ll refer to it as `max<T>`. In the next lesson, we’ll look at how we use our `max<T>` function template to generate one or more `max()` functions with parameters of different types.

```
#include <iostream>

template <typename T>

T add(T x, T y) {
	return x + y;
}

int main()
{
	std::cout << add(5.3, 2.0);
}
```

I made this function and it will output any numbers I add together of any type. U see i change the Return type and arguments type to be the TypeName T that I defined earlier so I can pass through any type and the compiler will figure out which type im using and return that value. In this code I pass thru double so imagine the compiler goes thru and replaces the T with double. 


Naming template parameters

Much like we often use a single letter for variable names used in trivial situations (e.g. `x`), it’s conventional to use a single capital letter (starting with `T`) when the template parameter is used in a trivial or obvious way. For example, in our `max` function template:

