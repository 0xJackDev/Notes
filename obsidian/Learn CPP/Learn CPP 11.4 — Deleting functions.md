
Deleting a function using the `= delete` specifier

In cases where we have a function that we explicitly do not want to be callable, we can define that function as deleted by using the **= delete** specifier. If the compiler matches a function call to a deleted function, compilation will be halted with a compile error.

Here’s an updated version of the above making use of this syntax:

```cpp
#include <iostream>

void printInt(int x)
{
    std::cout << x << '\n';
}

void printInt(char) = delete; // calls to this function will halt compilation
void printInt(bool) = delete; // calls to this function will halt compilation

int main()
{
    printInt(97);   // okay

    printInt('a');  // compile error: function deleted
    printInt(true); // compile error: function deleted

    printInt(5.0);  // compile error: ambiguous match

    return 0;
}
```

Copy

Let’s take a quick look at some of these. First, `printInt('a')` is a direct match for `printInt(char)`, which is deleted. The compiler thus produces a compilation error. `printInt(true)` is a direct match for `printInt(bool)`, which is deleted, and thus also produces a compilation error.

`printInt(5.0)` is an interesting case, with perhaps unexpected results. First, the compiler checks to see if exact match `printInt(double)` exists. It does not. Next, the compiler tries to find a best match. Although `printInt(int)` is the only non-deleted function, the deleted functions are still considered as candidates in function overload resolution. Because none of these functions are unambiguously the best match, the compiler will issue an ambiguous match compilation error.

Key insight

`= delete` means “I forbid this”, not “this doesn’t exist”.

Deleted function participate in all stages of function overload resolution (not just in the exact match stage). If a deleted function is selected, then a compilation error results.



