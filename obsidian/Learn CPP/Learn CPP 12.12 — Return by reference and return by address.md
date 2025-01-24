Return by reference

In cases where we’re passing a class type back to the caller, we may (or may not) want to return by reference instead. **Return by reference** returns a reference that is bound to the object being returned, which avoids making a copy of the return value. To return by reference, we simply define the return value of the function to be a reference type:

```cpp
std::string&       returnByReference(); // returns a reference to an existing std::string (cheap)
const std::string& returnByReferenceToConst(); // returns a const reference to an existing std::string (cheap)
```

Copy

Here is an academic program to demonstrate the mechanics of return by reference:

```cpp
#include <iostream>
#include <string>

const std::string& getProgramName() // returns a const reference
{
    static const std::string s_programName { "Calculator" }; // has static duration, destroyed at end of program

    return s_programName;
}

int main()
{
    std::cout << "This program is named " << getProgramName();

    return 0;
}
```

Copy

This program prints:

This program is named Calculator

Because `getProgramName()` returns a const reference, when the line `return s_programName` is executed, `getProgramName()` will return a const reference to `s_programName` (thus avoiding making a copy). That const reference can then be used by the caller to access the value of `s_programName`, which is printed.

The difference between the two is the above one makes it static so it exists after the function is over the below one isnt static so as soon as the function is destroyed so is the s_programName variable.


The object being returned by reference must exist after the function returns

Using return by reference has one major caveat: the programmer _must_ be sure that the object being referenced outlives the function returning the reference. Otherwise, the reference being returned will be left dangling (referencing an object that has been destroyed), and use of that reference will result in undefined behavior.

In the program above, because `s_programName` has static duration, `s_programName` will exist until the end of the program. When `main()` accesses the returned reference, it is actually accessing `s_programName`, which is fine, because `s_programName` won’t be destroyed until later.

Now let’s modify the above program to show what happens in the case where our function returns a dangling reference:

```cpp
#include <iostream>
#include <string>

const std::string& getProgramName()
{
    const std::string programName { "Calculator" }; // now a non-static local variable, destroyed when function ends

    return programName;
}

int main()
{
    std::cout << "This program is named " << getProgramName(); // undefined behavior

    return 0;
}
```

Copy

The result of this program is undefined. When `getProgramName()` returns, a reference bound to local variable `programName` is returned. Then, because `programName` is a local variable with automatic duration, `programName` is destroyed at the end of the function. That means the returned reference is now dangling, and use of `programName` in the `main()` function results in undefined behavior.

Modern compilers will produce a warning or error if you try to return a local variable by reference (so the above program may not even compile), but compilers sometimes have trouble detecting more complicated cases.

Warning

Objects returned by reference must live beyond the scope of the function returning the reference, or a dangling reference will result. Never return a (non-static) local variable or temporary by reference.


Return by address

**Return by address** works almost identically to return by reference, except a pointer to an object is returned instead of a reference to an object. Return by address has the same primary caveat as return by reference -- the object being returned by address must outlive the scope of the function returning the address, otherwise the caller will receive a dangling pointer.

The major advantage of return by address over return by reference is that we can have the function return `nullptr` if there is no valid object to return. For example, let’s say we have a list of students that we want to search. If we find the student we are looking for in the list, we can return a pointer to the object representing the matching student. If we don’t find any students matching, we can return `nullptr` to indicate a matching student object was not found.

The major disadvantage of return by address is that the caller has to remember to do a `nullptr` check before dereferencing the return value, otherwise a null pointer dereference may occur and undefined behavior will result. Because of this danger, return by reference should be preferred over return by address unless the ability to return “no object” is needed.


