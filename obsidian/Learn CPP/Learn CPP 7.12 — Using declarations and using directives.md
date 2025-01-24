

Qualified and unqualified names

A name can be either qualified or unqualified.

A **qualified name** is a name that includes an associated scope. Most often, names are qualified with a namespace using the scope resolution operator (::). For example:

```cpp
std::cout // identifier cout is qualified by namespace std
::foo // identifier foo is qualified by the global namespace
```


An **unqualified name** is a name that does not include a scoping qualifier. For example, `cout` and `x` are unqualified names, as they do not include an associated scope.


Using-declarations

One way to reduce the repetition of typing `std::` over and over is to utilize a using-declaration statement. A **using declaration** allows us to use an unqualified name (with no scope) as an alias for a qualified name.

Here’s our basic Hello world program, using a using-declaration on line 5:

```cpp
#include <iostream>

int main()
{
   using std::cout; // this using declaration tells the compiler that cout should resolve to std::cout
   cout << "Hello world!\n"; // so no std:: prefix is needed here!

   return 0;
} // the using declaration expires at the end of the current scope
```

Copy

The using-declaration `using std::cout;` tells the compiler that we’re going to be using the object `cout` from the `std` namespace. So whenever it sees `cout`, it will assume that we mean `std::cout`. If there’s a naming conflict between `std::cout` and some other use of `cout`, `std::cout` will be preferred. Therefore on line 6, we can type `cout` instead of `std::cout`.

This doesn’t save much effort in this trivial example, but if you are using `cout` many times inside of a function, a using-declaration can make your code more readable. Note that you will need a separate using-declaration for each name (e.g. one for `std::cout`, one for `std::cin`, etc…).

The using-declaration is active from the point of declaration to the end of the scope in which it is declared.

Although using-declarations are less explicit than using the `std::` prefix, they are generally considered safe and acceptable to use in source (.cpp) files, after the #includes (particularly inside functions).



Using-directives

Another way to simplify things is to use a using-directive. A **using directive** allows _all_ identifiers in a given namespace to be referenced without qualification from the scope of the using-directive.

Here’s our Hello world program again, with a using-directive on line 5:

```cpp
#include <iostream>

int main()
{
   using namespace std; // all names from std namespace now accessible without qualification
   cout << "Hello world!\n"; // so no std:: prefix is needed here

   return 0;
} // the using-directive ends at the end of the current scope
```

Copy

The using-directive `using namespace std;` tells the compiler that all of the names in the `std` namespace should be accessible without qualification in the current scope (in this case, of function `main()`). When we then use unqualified identifier `cout`, it will resolve to `std::cout`.

Using-directives are the solution that was provided for old pre-namespace codebases that used unqualified names for standard library functionality. Rather than having to manually update every unqualified name to a qualified name (which was risky), a single using-directive (`using namespace std;`) could be placed at the top of each file, and all of the names that had been moved to the `std` namespace could still be used unqualified.




## Problems with using-directives (a.k.a. why you should avoid “using namespace std;”) [](https://www.learncpp.com/cpp-tutorial/using-declarations-and-using-directives/#avoidUsingNamespace)



In modern C++, using-directives generally offer little benefit (saving some typing) compared to the risk. This is due to two factors:

1. Using-directives allow unqualified access to _all_ of the names from a namespace (potentially including lots of names you’ll never use).
2. Using-directives do not prefer names from the namespace of the using-directive over other names.

The end result is that the possibility for naming collisions to occur increases significantly (especially if you import the `std` namespace).

For illustrative purposes, let’s take a look at an example where using-directives cause ambiguity:

```cpp
#include <iostream>

namespace a
{
	int x{ 10 };
}

namespace b
{
	int x{ 20 };
}

int main()
{
	using namespace a;
	using namespace b;

	std::cout << x << '\n';

	return 0;
}
```

Copy

In the above example, the compiler is unable to determine whether the `x` in `main` refers to `a::x` or `b::x`. In this case, it will fail to compile with an “ambiguous symbol” error. We could resolve this by removing one of the using-statements, employing a using-declaration instead, or qualifying `x` with an explicit scope qualifier (`a::` or `b::`).



Here’s another more subtle example:

```cpp
#include <iostream> // imports the declaration of std::cout

int cout() // declares our own "cout" function
{
    return 5;
}

int main()
{
    using namespace std; // makes std::cout accessible as "cout"
    cout << "Hello, world!\n"; // uh oh!  Which cout do we want here?  The one in the std namespace or the one we defined above?

    return 0;
}
```

Copy

In the above example, the compiler is unable to determine whether our unqualified use of `cout` means `std::cout` or the `cout` function we’ve defined, and again will fail to compile with an “ambiguous symbol” error. Although this example is trivial, if we had explicitly prefixed `std::cout` like this:

```cpp
std::cout << "Hello, world!\n"; // tell the compiler we mean std::cout
```

Copy

or used a using-declaration instead of a using-directive:

```cpp
using std::cout; // tell the compiler that cout means std::cout
cout << "Hello, world!\n"; // so this means std::cout
```




The scope of using-declarations and using-directives

If a using-declaration or using-directive is used within a block, the names are applicable to just that block (it follows normal block scoping rules). This is a good thing, as it reduces the chances for naming collisions to occur to just within that block.

If a using-declaration or using-directive is used in the global namespace, the names are applicable to the entire rest of the file (they have file scope).

Cancelling or replacing a using-statement

Once a using-statement has been declared, there’s no way to cancel or replace it with a different using-statement within the scope in which it was declared. the best u can do is limit the scope


Best practices for using-statements

Avoid using-directives (particularly `using namespace std;`) altogether, except in specific circumstances (such as `using namespace std::literals` to access the `s` and `sv` literal suffixes).

Using-declarations are generally considered safe to use inside functions. Avoid using them in namespaces, especially the global namespace of a header file.

Best practice

Prefer explicit namespace qualifiers over using-statements. Avoid using-directives altogether (except `using namespace std::literals`). Using-declarations are okay to use in .cpp files, after the #includes.