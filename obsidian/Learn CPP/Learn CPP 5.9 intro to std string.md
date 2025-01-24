


In lesson [5.2 -- Literals](https://www.learncpp.com/cpp-tutorial/literals/), we introduced C-style string literals:

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, world!"; // "Hello world!" is a C-style string literal.
    return 0;
}
```

Copy

While C-style string literals are fine to use, C-style string variables behave oddly, are hard to work with (e.g. you can’t use assignment to assign a C-style string variable a new value), and are dangerous (e.g. if you copy a larger C-style string into the space allocated for a shorter C-style string, undefined behavior will result). In modern C++, C-style string variables are best avoided.



C++ has introduced two additional string types into the language. std::string and std::string_view. 
Unlike the types we have introduced previously std::string and std::string_view arent fundamental types they are instead class types but basic usage of each is straightforward


## INTRO TO STD::STRING

the easiest ways to work with strings and string objects in C++ is via the std::string type which lives in the 


```cpp
#include <string> // allows use of std::string

int main()
{
    std::string name {}; // empty string

    return 0;
}
```


you dont really need to include the string header if u include iostream tho.


Just like normal variables, you can initialize or assign values to std::string objects as you would expect:

```cpp
#include <string>

int main()
{
    std::string name { "Alex" }; // initialize name with string literal "Alex"
    name = "John";               // change name to "John"

    return 0;
}
```

Copy

Note that strings can be composed of numeric characters as well:

```cpp
std::string myID{ "45" }; // "45" is not the same as integer 45!
```


in string form numbers are treated as text and not numbers so they cant be manipulated as numbers (e.g. you cant multiply them) C++ will not automatically convert strings to integers or floating point values.



std::string works exactly as expected with std::cout


`std::string` can handle strings of different lengths

One of the neatest things that `std::string` can do is store strings of different lengths:

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string name { "Alex" }; // initialize name with string literal "Alex"
    std::cout << name << '\n';

    name = "Jason";              // change name to a longer string
    std::cout << name << '\n';

    name = "Jay";                // change name to a shorter string
    std::cout << name << '\n';

    return 0;
}
```

Copy

This prints:

Alex
Jason
Jay

In the above example, `name` is initialized with the string `"Alex"`, which contains five characters (four explicit characters and a null-terminator). We then set `name` to a larger string, and then a smaller string. `std::string` has no problem handling this! You can even store really long strings in a `std::string`.

This is one of the reasons that `std::string` is so powerful.


Key insight

If `std::string` doesn’t have enough memory to store a string, it will request additional memory (at runtime) using a form of memory allocation known as dynamic memory allocation. This ability to acquire additional memory is part of what makes `std::string` so flexible, but also comparatively slow.

We cover dynamic memory allocation in a future chapter.



String input with `std::cin`

Using `std::string` with `std::cin` may yield some surprises! Consider the following example:

```cpp
#include <iostream>
#include <string>

int main()
{
    std::cout << "Enter your full name: ";
    std::string name{};
    std::cin >> name; // this won't work as expected since std::cin breaks on whitespace

    std::cout << "Enter your favorite color: ";
    std::string color{};
    std::cin >> color;

    std::cout << "Your name is " << name << " and your favorite color is " << color << '\n';

    return 0;
}
```

Copy

Here’s the results from a sample run of this program:

Enter your full name: John Doe
Enter your favorite color: Your name is John and your favorite color is Doe

Hmmm, that isn’t right! What happened? It turns out that when using `operator>>` to extract a string from `std::cin`, `operator>>` only returns characters up to the first whitespace it encounters. Any other characters are left inside `std::cin`, waiting for the next extraction.

So when we used `operator>>` to extract input into variable `name`, only `"John"` was extracted, leaving `" Doe"` inside `std::cin`. When we then used `operator>>` to get extract input into variable `color`, it extracted `"Doe"` instead of waiting for us to input an color. Then the program ends.



so instead of using std::cin we should use

## use std::getline() to input text.

```

#include <iostream>
#include <string>

int main() {
	std::cout << "enter your full name";
	std::string name{};
	std::getline(std::cin >> std::ws, name);

	std::cout << "Enter your favorite color: ";
	std::string color{};
	std::getline(std::cin >> std::ws, color); // read a full line of text into color

	std::cout << "Your name is " << name << " and your favorite color is " << color << '\n';

	return 0;
}
```

for example this would make a Program that asks a user for his full name and color and outputs it


## Wait what the fuck is std::ws?


In lesson [4.8 -- Floating point numbers](https://www.learncpp.com/cpp-tutorial/floating-point-numbers/), we discussed output manipulators, which allow us to alter the way output is displayed. In that lesson, we used the output manipulator function `std::setprecision()` to change the number of digits of precision that `std::cout` displayed.

C++ also supports input manipulators, which alter the way that input is accepted. The `std::ws` input manipulator tells `std::cin` to ignore any leading whitespace before extraction. Leading whitespace is any whitespace character (spaces, tabs, newlines) that occur at the start of the string.

(std:: white space)
Let’s explore why this is useful. Consider the following program:

```cpp
#include <iostream>
#include <string>

int main()
{
    std::cout << "Pick 1 or 2: ";
    int choice{};
    std::cin >> choice;

    std::cout << "Now enter your name: ";
    std::string name{};
    std::getline(std::cin, name); // note: no std::ws here

    std::cout << "Hello, " << name << ", you picked " << choice << '\n';

    return 0;
}
```

Copy

Here’s some output from this program:

Pick 1 or 2: 2
Now enter your name: Hello, , you picked 2

This program first asks you to enter 1 or 2, and waits for you to do so. All good so far. Then it will ask you to enter your name. However, it won’t actually wait for you to enter your name! Instead, it prints the “Hello” string, and then exits.

When you enter a value using `operator>>`, `std::cin` not only captures the value, it also captures the newline character (`'\n'`) that occurs when you hit the enter key. So when we type `2` and then hit enter, `std::cin` captures the string `"2\n"` as input. It then extracts the value `2` to variable `choice`, leaving the newline character behind for later. Then, when `std::getline()` goes to extract text to `name`, it sees `"\n"` is already waiting in `std::cin`, and figures we must have previously entered an empty string! Definitely not what was intended.

We can amend the above program to use the `std::ws` input manipulator, to tell `std::getline()` to ignore any leading whitespace characters:



```cpp
#include <iostream>
#include <string>

int main()
{
    std::cout << "Pick 1 or 2: ";
    int choice{};
    std::cin >> choice;

    std::cout << "Now enter your name: ";
    std::string name{};
    std::getline(std::cin >> std::ws, name); // note: added std::ws here

    std::cout << "Hello, " << name << ", you picked " << choice << '\n';

    return 0;
}
```


The length of a `std::string`

If we want to know how many characters are in a `std::string`, we can ask a `std::string` object for its length. The syntax for doing this is different than you’ve seen before, but is pretty straightforward:

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string name{ "Alex" };
    std::cout << name << " has " << name.length() << " characters\n";

    return 0;
}
```

Copy

This prints:

Alex has 4 characters

Although `std::string` is required to be null-terminated (as of C++11), the returned length of a `std::string` does not include the implicit null-terminator character.

Note that instead of asking for the string length as `length(name)`, we say `name.length()`. The `length()` function isn’t a normal standalone function -- it’s a special type of function that is nested within `std::string` called a _member function_. Because the `length()` member function is declared inside of `std::string`, it is sometimes written as `std::string::length()` in documentation.

We’ll cover member functions, including how to write your own, in more detail later.


Also note that `std::string::length()` returns an unsigned integral value (most likely of type `size_t`). If you want to assign the length to an `int` variable, you should `static_cast` it to avoid compiler warnings about signed/unsigned conversions:

```cpp
int length { static_cast<int>(name.length()) };
```

Copy

In C++20, you can also use the `std::ssize()` function to get the length of a `std::string` as a large signed integral type (usually `std::ptrdiff_t`):

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string name{ "Alex" };
    std::cout << name << " has " << std::ssize(name) << " characters\n";

    return 0;
}
```

Copy

Since a `ptrdiff_t` may be larger than an `int`, if you want to store the result of `std::ssize()` in an `int` variable, you should `static_cast` the result to an `int`:

```cpp
int len { static_cast<int>(std::ssize(name)) };
```

Copy

Initializing a `std::string` is expensive

Whenever a std::string is initialized, a copy of the string used to initialize it is made. Making copies of strings is expensive, so care should be taken to minimize the number of copies made.

Do not pass `std::string` by value

When a `std::string` is passed to a function by value, the `std::string` function parameter must be instantiated and initialized with the argument. This results in an expensive copy. We’ll discuss what to do instead (use `std::string_view`) in lesson [5.10 -- Introduction to std::string_view](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring_view/).

Best practice

Do not pass `std::string` by value, as it makes an expensive copy.

Tip

In most cases, use a `std::string_view` parameter instead (covered in lesson [5.10 -- Introduction to std::string_view](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring_view/)).



Returning a `std::string`

When a function returns by value to the caller, the return value is normally copied from the function back to the caller. So you might expect that you should not return `std::string` by value, as doing so would return an expensive copy of a `std::string`.

However, as a rule of thumb, it is okay to return a `std::string` by value when the expression of the return statement resolves to any of the following:

- A local variable of type `std::string`.
- A `std::string` that has been returned by value from another function call or operator.
- A `std::string` temporary that is created as part of the return statement.
in most cases avoid returning a std::string by value

Literals for `std::string`

Double-quoted string literals (like “Hello, world!”) are C-style strings by default (and thus, have a strange type).

We can create string literals with type `std::string` by using a `s` suffix after the double-quoted string literal. The `s` must be lower case.

```cpp
#include <iostream>
#include <string> // for std::string

int main()
{
    using namespace std::string_literals; // easy access to the s suffix

    std::cout << "foo\n";   // no suffix is a C-style string literal
    std::cout << "goo\n"s;  // s suffix is a std::string literal

    return 0;
}
```



Constexpr strings [](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring/#constexprStrings)

If you try to define a `constexpr std::string`, your compiler will probably generate an error:


Conclusion

`std::string` is complex, leveraging many language features that we haven’t covered yet. Fortunately, you don’t need to understand these complexities to use `std::string` for simple tasks, like basic string input and output. We encourage you to start experimenting with strings now, and we’ll cover additional string capabilities later.