

Now consider this similar program:

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string s{ "Hello, world!" }; // s makes a copy of its initializer
    std::cout << s << '\n';

    return 0;
}
```

Copy

When `s` is initialized, the C-style string literal `"Hello, world!"` is copied into memory allocated for `std::string s`. Unlike fundamental types, initializing and copying a `std::string` is slow.

In the above program, all we do with `s` is print the value to the console, and then `s` is destroyed. We’ve essentially made a copy of “Hello, world!” just to print and then destroy that copy. That’s inefficient.

We see something similar in this example:

```cpp
#include <iostream>
#include <string>

void printString(std::string str) // str makes a copy of its initializer
{
    std::cout << str << '\n';
}

int main()
{
    std::string s{ "Hello, world!" }; // s makes a copy of its initializer
    printString(s);

    return 0;
}
```

Copy

This example makes two copies of the C-style string “Hello, world!”: one when we initialize `s` in `main()`, and another when we initialize parameter `str` in `printString()`. That’s a lot of needless copying just to print a string!



## std::string_view

To address the issue with std::string being slow and expensive to initialize. C++ 17 introduced std::string_view which lives in the <string_view> header. std::string_view provides read_only access to an existing string. whether a C style string or std::string or another std::string_view. Without making a copy. Read only means we can access the value and use the value being viewed but cant modify the value. 


```
#include <iostream>
#include <string>
#include <string_view>


void printStringView(std::string_view str) {
	std::cout << str << '\n';
}

int main()
{
	std::string s{ "Hello world" };
	printStringView(s);

}

```

std::string_view str this part of the function may look like its defining two different variables but really the std::string_view is the type and the the identifier is str. 
Also to use this make sure your Using C++ 17 or higher. I will now on use C++ 20 cause why wouldnt i?


This program produces the same output as the prior one, but no copies of the string “Hello, world!” are made.

When we initialize `std::string_view s` with C-style string literal `"Hello, world!"`, `s` provides read-only access to “Hello, world!” without making a copy of the string. When we pass `s` to `printSV()`, parameter `str` is initialized from `s`. This allows us to access “Hello, world!” through `str`, again without making a copy of the string.

*best practice is to use std::string_view over std::string when u need a read only string especially for function parameters*



`std::string_view` can be initialized with many different types of strings

One of the neat things about a `std::string_view` is how flexible it is. A `std::string_view` object can be initialized with a C-style string, a `std::string`, or another `std::string_view`:

```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    std::string_view s1 { "Hello, world!" }; // initialize with C-style string literal
    std::cout << s1 << '\n';

    std::string s{ "Hello, world!" };
    std::string_view s2 { s };  // initialize with std::string
    std::cout << s2 << '\n';

    std::string_view s3 { s2 }; // initialize with std::string_view
    std::cout << s3 << '\n';

    return 0;
}
```

Copy

`std::string_view` parameters will accept many different types of string arguments

Both a C-style string and a `std::string` will implicitly convert to a `std::string_view`. Therefore, a `std::string_view` parameter will accept arguments of type C-style string, a `std::string`, or `std::string_view`:

```cpp
#include <iostream>
#include <string>
#include <string_view>

void printSV(std::string_view str)
{
    std::cout << str << '\n';
}

int main()
{
    printSV("Hello, world!"); // call with C-style string literal

    std::string s2{ "Hello, world!" };
    printSV(s2); // call with std::string

    std::string_view s3 { s2 };
    printSV(s3); // call with std::string_view

    return 0;
}
```



std::string_view only makes a copy of the initializer. So since std::string is very expensive. C++ doesn't allow implicit conversion of std::string_view to std::string this is to prevent passing a string_view argument to a std::string parameter, and making a copy that isnt desired.

However, if this is desired, we have two options:

1. Explicitly create a `std::string` with a `std::string_view` initializer (which is allowed, since this will rarely be done unintentionally)
2. Convert an existing `std::string_view` to a `std::string` using `static_cast`

The following example shows both options:

```cpp
#include <iostream>
#include <string>
#include <string_view>

void printString(std::string str)
{
	std::cout << str << '\n';
}

int main()
{
	std::string_view sv{ "Hello, world!" };

	// printString(sv);   // compile error: won't implicitly convert std::string_view to a std::string

	std::string s{ sv }; // okay: we can create std::string using std::string_view initializer
	printString(s);      // and call the function with the std::string

	printString(static_cast<std::string>(sv)); // okay: we can explicitly cast a std::string_view to a std::string

	return 0;
}
```


Assignment changes what the `std::string_view` is viewing

Assigning a new string to a `std::string_view` causes the `std::string_view` to view the new string. It does not modify the prior string being viewed in any way.

Literals for `std::string_view`

Double-quoted string literals are C-style string literals by default. We can create string literals with type `std::string_view` by using a `sv` suffix after the double-quoted string literal. The `sv` must be lower case.

```cpp
#include <iostream>
#include <string>      // for std::string
#include <string_view> // for std::string_view

int main()
{
    using namespace std::string_literals;      // access the s suffix
    using namespace std::string_view_literals; // access the sv suffix

    std::cout << "foo\n";   // no suffix is a C-style string literal
    std::cout << "goo\n"s;  // s suffix is a std::string literal
    std::cout << "moo\n"sv; // sv suffix is a std::string_view literal

    return 0;
}
```

Copy

Related content

We discuss this use of `using namespace` in lesson [5.9 -- Introduction to std::string](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring/). The same advice applies here.

It’s fine to initialize a `std::string_view` object with a C-style string literal (you don’t need to initialize it with a `std::string_view` literal).

That said, initializing a `std::string_view` using a `std::string_view` literal won’t cause problems (as such literals are actually C-style string literals in disguise).



constexpr `std::string_view`

Unlike `std::string`, `std::string_view` has full support for constexpr:

```cpp
#include <iostream>
#include <string_view>

int main()
{
    constexpr std::string_view s{ "Hello, world!" }; // s is a string symbolic constant
    std::cout << s << '\n'; // s will be replaced with "Hello, world!" at compile-time

    return 0;
}
```

Copy

This makes `constexpr std::string_view` the preferred choice when string symbolic constants are needed.

We will continue discussing `std::string_view` in the next lesson.




Part 2:


Viewing is inexpensive. As a viewer, you have no responsibility for the objects you are viewing, but you also have no control over those objects.



## std::string is an owner. 
This is why std::string is expensive. Because when a object is instantiated memory is allocated for that object to store whatever data it needs to use throughout its lifetime. The memory is reserved for the object and guaranteed to exist for as long as the object does. It is a a safe space. std::string and most other objects copy the initialization value its given into memory so it has its own independent value to access and manipulated later. Once the initialization value has be copied the object is no longer reliant on the initialization in any way.

And that’s a good thing, because the initializer generally can’t be trusted after initialization is complete. If you imagine the initialization process as a function call that initializes the object, who is passing in the initializer? The caller. When initialization is done, control returns back to the caller. At this point, the initialization statement is complete, and one of two things will typically happen:

- If the initializer was a temporary value or object, that temporary will be destroyed immediately.
- If the initializer was a variable, the caller still has access to that object. The caller can then do whatever it wants with the object, including modify or destroy it.


Because `std::string` makes its own copy of the value, it doesn’t have to worry about what happens after initialization is finished. The initializer can be destroyed, or modified, and it doesn’t affect the `std::string`. The downside is that this independence comes with the cost of an expensive copy.


In this context std::string is an owner 



## we dont always need a copy

Let’s revisit this example from the prior lesson:

```cpp
#include <iostream>
#include <string>

void printString(std::string str) // str makes a copy of its initializer
{
    std::cout << str << '\n';
}

int main()
{
    std::string s{ "Hello, world!" };
    printString(s);

    return 0;
}
```

Copy

When `printString(s)` is called, `str` makes an expensive copy of `s`. The function prints the copied string and then destroys it.

Note that `s` is already holding the string we want to print. Could we just use the string that `s` is holding instead of making a copy? The answer is possibly -- there are three criteria we need to assess:

- Could `s` be destroyed while `str` is still using it? No, `str` dies at the end of the function, and `s` exists in the scope of the caller and can’t be destroyed before the function returns.
- Could `s` be modified while `str` is still using it? No, `str` dies at the end of the function, and the caller has no opportunity to modify the `s` before the function returns.
- Does `str` modify the string in some way that the caller would not expect? No, the function does not modify the string at all.

Since all three of these criteria are false, there is no risk in using the string that `s` is holding instead of making a copy. And since string copies are expensive, why pay for one that we don’t need?



## std::view is a viewer


`std::string_view` takes a different approach to initialization. Instead of making an expensive copy of the initialization string, `std::string_view` creates an inexpensive view _of_ the initialization string. The `std::string_view` can then be used whenever access to the string is required.

In the context of our analogy, `std::string_view` is a viewer. It views an object that already exists elsewhere, and cannot modify that object. When the view is destroyed, the object being viewed is not affected.

It is important to note that a `std::string_view` remains dependent on the initializer through its lifetime. If the string being viewed is modified or destroyed while the view is still being used, unexpected or undefined behavior will result.

Whenever we use a view, it is up to us to ensure these possibilities do not occur.

Warning

A view is dependent on the object being viewed. If the object being viewed is modified or destroyed while the view is still being used, unexpected or undefined behavior will result.

A `std::string_view` that is viewing a string that has been destroyed is sometimes called a **dangling** view




## std::string is best used as a read only function parameter 





Should I prefer `std::string_view` or `const std::string&` function parameters? Advanced

Prefer `std::string_view` in most cases. We cover this topic further in lesson [12.6 -- Pass by const lvalue reference](https://www.learncpp.com/cpp-tutorial/pass-by-const-lvalue-reference/#stringparameter).


## Improperly using `std::string_view`

Let’s take a look at a few cases where misusing `std::string_view` gets us into trouble.

Here’s our first example:

```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    std::string_view sv{};

    { // create a nested block
        std::string s{ "Hello, world!" }; // create a std::string local to this nested block
        sv = s; // sv is now viewing s
    } // s is destroyed here, so sv is now viewing an invalid string

    std::cout << sv << '\n'; // undefined behavior

    return 0;
}
```

Copy

In this example, we’re creating `std::string s` inside a nested block (don’t worry about what a nested block is yet). Then we set `sv` to view `s`. `s` is then destroyed at the end of the nested block. `sv` doesn’t know that `s` has been destroyed. When we then use `sv`, we are accessing an invalid object, and undefined behavior results.




Here’s another variant of the same issue, where we initialize a `std::string_view` with the `std::string` return value of a function:

```cpp
#include <iostream>
#include <string>
#include <string_view>

std::string getName()
{
    std::string s { "Alex" };
    return s;
}

int main()
{
  std::string_view name { getName() }; // name initialized with return value of function
  std::cout << name << '\n'; // undefined behavior

  return 0;
}
```

Copy

This behaves similarly to the prior example. The `getName()` function is returning a `std::string` containing the string “Alex”. Return values are temporary objects that are destroyed at the end of the full expression containing the function call. We must either use this return value immediately, or copy it to use later.

But `std::string_view` doesn’t make copies. Instead, it creates a view to the temporary return value, which is then destroyed. That leaves our `std::string_view` dangling (viewing an invalid object), and printing the view results in undefined behavior.


The following is a less-obvious variant of the above:

```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    using namespace std::string_literals;
    std::string_view name { "Alex"s }; // "Alex"s creates a temporary std::string
    std::cout << name << '\n'; // undefined behavior

    return 0;
}
```

Copy

A `std::string` literal (created via the `s` literal suffix) creates a temporary `std::string` object. So in this case, `"Alex"s` creates a temporary `std::string`, which we then use as the initializer for `name`. At this point, `name` is viewing the temporary `std::string`. Then the temporary `std::string` is destroyed, leaving `name` dangling. We get undefined behavior when we then use `name`.

Warning

Do not initialize a `std::string_view` with a `std::string` literal, as this will leave the `std::string_view` dangling.

It is okay to initialize a `std::string_view` with a C-style string literal or a `std::string_view` literal. It’s also okay to initialize a `std::string_view` with a C-style string object, a `std::string` object, or a `std::string_view` object, as long as that string object outlives the view.



We can also get undefined behavior when the underlying string is modified:


*Key insight

*Modifying a `std::string` invalidates all views into that `std::string`.*





Revalidating an invalid `std::string_view`

to do this just be after changed the value of the string make sure that u redefine the string_view to that variable again.

Invalidated objects can often be revalidated (made valid again) by setting them back to a known good state. For an invalidated `std::string_view`, we can do this by assigning the invalidated `std::string_view` object a valid string to view.

Here’s the same example as prior, but we’ll revalidate `sv`:

```cpp
#include <iostream>
#include <string>
#include <string_view>

int main()
{
    std::string s { "Hello, world!" };
    std::string_view sv { s }; // sv is now viewing s

    s = "Hello, universe!";    // modifies s, which invalidates sv (s is still valid)
    std::cout << sv << '\n';   // undefined behavior

    sv = s;                    // revalidate sv: sv is now viewing s again
    std::cout << sv << '\n';   // prints "Hello, universe!"

    return 0;
}
```

Copy

After `sv` is invalidated by the modification of `s`, we revalidate `sv` via the statement `sv = s`, which causes `sv` to become a valid view of `s` again. When we print `sv` the second time, it prints “Hello, universe!”.

## Be careful returning a `std::string_view`


`std::string_view` can be used as the return value of a function. However, this is often dangerous.

Because local variables are destroyed at the end of the function, returning a `std::string_view` to a local variable will result in the returned `std::string_view` being invalid, and further use of that `std::string_view` will result in undefined behavior. For example:

```cpp
#include <iostream>
#include <string>
#include <string_view>

std::string_view getBoolName(bool b)
{
    std::string t { "true" };  // local variable
    std::string f { "false" }; // local variable

    if (b)
        return t;  // return a std::string_view viewing t

    return f; // return a std::string_view viewing f
} // t and f are destroyed at the end of the function

int main()
{
    std::cout << getBoolName(true) << ' ' << getBoolName(false) << '\n'; // undefined behavior

    return 0;
}
```



In the above example it creates two string variables named t ans f but when it returns those it returns them as a string_view but they are viewing the variables created inside the function so once u leave that function the return has no longer the Orignal variable to look at anymore resulting in undefined behavior

Your compiler may or may not warn you about such cases.


There are two main cases where a `std::string_view` can be returned safely. First, because C-style string literals exist for the entire program, it’s fine (and useful) to return C-style string literals from a function that has a return type of `std::string_view`.

```cpp
#include <iostream>
#include <string_view>

std::string_view getBoolName(bool b)
{
    if (b)
        return "true";  // return a std::string_view viewing "true"

    return "false"; // return a std::string_view viewing "false"
} // "true" and "false" are not destroyed at the end of the function

int main()
{
    std::cout << getBoolName(true) << ' ' << getBoolName(false) << '\n'; // ok

    return 0;
}
```

Copy

This prints:

true false



When `getBoolName(true)` is called, the function will return a `std::string_view` viewing the C-style string `"true"`. Because `"true"` exists for the entire program, there’s no problem when we use the returned `std::string_view` to print `"true"` within `main()`.




Second, it is generally okay to return a function parameter of type `std::string_view`:

```cpp
#include <iostream>
#include <string>
#include <string_view>

std::string_view firstAlphabetical(std::string_view s1, std::string_view s2)
{
    return s1 < s2 ? s1: s2; // uses operator?: (the conditional operator)
}

int main()
{
    std::string a { "World" };
    std::string b { "Hello" };

    std::cout << firstAlphabetical(a, b) << '\n'; // prints "Hello"

    return 0;
}
```

Copy

It may be less obvious why this is okay. First, note that arguments `a` and `b` exist in the scope of the caller. When the function is called, function parameter `s1` is a view into `a`, and function parameter `s2` is a view into `b`. When the function returns either `s1` or `s2`, it is returning a view into `a` or `b` back to the caller. Since `a` and `b` still exist at this point, it’s fine to use the returned `std::string_view` into `a` or `b`.

There is one important subtlety here. If the argument is a temporary object (that will be destroyed at the end of the full expression containing the function call), the `std::string_view` return value must be used in the same expression. After that point, the temporary is destroyed and the std::string_view is left dangling.





## view modification functions

Because `std::string_view` is a view, it contains functions that let us modify our view by “closing the curtains”. This does not modify the string being viewed in any way, just the view itself.

- The `remove_prefix()` member function removes characters from the left side of the view.
- The `remove_suffix()` member function removes characters from the right side of the view.

```cpp
#include <iostream>
#include <string_view>

int main()
{
	std::string_view str{ "Peach" };
	std::cout << str << '\n';

	// Remove 1 character from the left side of the view
	str.remove_prefix(1);
	std::cout << str << '\n';

	// Remove 2 characters from the right side of the view
	str.remove_suffix(2);
	std::cout << str << '\n';

	str = "Peach"; // reset the view
	std::cout << str << '\n';

	return 0;
}
```

Copy

This program produces the following output:

Peach
each
ea
Peach


For example 

```
#include <iostream>
#include <string>
#include <string_view>


void printStringView(std::string_view str) {
	str.remove_suffix(5);
	std::cout << str << std::endl;
}

int main()
{
	std::string s{ "Hello world" };
	printStringView(s);

}

```
```

this will simply print hello as it removes the last 5 words of the string. Not including the Null/ terminator operator \0
	std::string s{ "Hel\0lo world" }; if i made a string like this btw it would just print Hel as the string terminates at \0
```



Unlike real curtains, once `remove_prefix()` and `remove_suffix()` have been called, the only way to reset the view is by reassigning the source string to it again.


`std::string_view` can view a substring

This brings up an important use of `std::string_view`. While `std::string_view` can be used to view an entire string without making a copy, they are also useful when we want to view a substring without making a copy. A **substring** is a contiguous sequence of characters within an existing string. For example, given the string “snowball”, some substrings are “snow”, “all”, and “now”. “owl” is not a substring of “snowball” because these characters do not appear contiguously in “snowball”.


`std::string_view` may or may not be null-terminated

The ability to view just a substring of a larger string comes with one consequence of note: a `std::string_view` may or may not be null-terminated.

Related content

We cover what a null-terminated string is in lesson [5.2 -- Literals](https://www.learncpp.com/cpp-tutorial/literals/).

Consider the string “snowball”, which is null-terminated (because it is a C-style string literal, which are always null-terminated). If a `std::string_view` views the whole string, then it is viewing a null-terminated string. However, if `std::string_view` is only viewing the substring “now”, then that substring is not null-terminated (the next character is a ‘b’).

Key insight

A C-style string literal and a `std::string` are always null-terminated.  
A `std::string_view` may or may not be null-terminated.



In almost all cases, this doesn’t matter -- a `std::string_view` keeps track of the length of the string or substring it is viewing, so it doesn’t need the null-terminator. Converting a `std::string_view` to a `std::string` will work regardless of whether or not the `std::string_view` is null-terminated.

Warning

Take care not to write any code that assumes a `std::string_view` is null terminated.



A quick guide on when to use `std::string` vs `std::string_view` [](https://www.learncpp.com/cpp-tutorial/stdstring_view-part-2/#stringvsstringview)

This guide is not meant to be comprehensive, but is intended to highlight the most common cases:

**Variables**

Use a `std::string` variable when:

- You need a string that you can modify.
- You need to store user-inputted text.
- You need to store the return value of a function that returns a `std::string`.

Use a `std::string_view` variable when:

- You need read-only access to part or all of a string that already exists elsewhere and will not be modified or destroyed before use of the `std::string_view` is complete.
- You need a symbolic constant for a C-style string.
- You need to continue viewing the return value of a function that returns a C-style string or a non-dangling `std::string_view`.

**Function parameters**

Use a `std::string` function parameter when:

- The function needs to modify the string passed in as an argument without affecting the caller. This is rare.
- You are using language standard C++14 or older and aren’t comfortable using references yet.

Use a `std::string_view` function parameter when:

- The function needs a read-only string.
- The function needs to work with non-null-terminated strings.


**Return types**

Use a `std::string` return type when:

- The return value is a `std::string` local variable or function parameter.
- The return value is a function call or operator that returns a `std::string` by value.

Use a `std::string_view` return type when:

- The function returns a C-style string literal or local `std::string_view` that has been initialized with a C-style string literal.
- The function returns a `std::string_view` parameter.