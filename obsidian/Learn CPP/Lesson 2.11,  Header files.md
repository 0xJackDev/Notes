As programs become larger it becomes annoying to forward declare every function you want to use that is defined in a different file so header files solve this problem

.cpp files are not the only files commonly seen in C++ programs. the other type is called a header files. Head files have a .h extension you will occasinally see .hpp or no extension though. The primary purpose is to declare functions to code.

The answer is that _std::cout_ has been forward declared in the “iostream” header file. When we `#include <iostream>`, we’re requesting that the preprocessor copy all of the content (including forward declarations for std::cout) from the file named “iostream” into the file doing the #include.

Header files only have two parts

1. A header guard (discussed later)
2. the actual content of the header file which is usually just a forward declaration for all of the identifiers we want other files to see


For now, you should avoid putting function or variable definitions in header files. Doing so will generally result in a violation of the one-definition rule (ODR) in cases where the header file is included into more than one source file.


Angled brackets vs double quotes [](https://www.learncpp.com/cpp-tutorial/header-files/#includemethod)

You’re probably curious why we use angled brackets for `iostream`, and double quotes for `add.h`. It’s possible that a header file with the same filename might exist in multiple directories. Our use of angled brackets vs double quotes helps give the preprocessor a clue as to where it should look for header files.

When we use angled brackets, we’re telling the preprocessor that this is a header file we didn’t write ourselves. The preprocessor will search for the header only in the directories specified by the `include directories`. The `include directories` are configured as part of your project/IDE settings/compiler settings, and typically default to the directories containing the header files that come with your compiler and/or OS. The preprocessor will not search for the header file in your project’s source code directory.


- Always include header guards (we’ll cover these next lesson).
- Do not define variables and functions in header files (for now).
- Give a header file the same name as the source file it’s associated with (e.g. `grades.h` is paired with `grades.cpp`).
- Each header file should have a specific job, and be as independent as possible. For example, you might put all your declarations related to functionality A in A.h and all your declarations related to functionality B in B.h. That way if you only care about A later, you can just include A.h and not get any of the stuff related to B.
- Be mindful of which headers you need to explicitly include for the functionality that you are using in your code files, to avoid inadvertent transitive includes.
- A header file should #include any other headers containing functionality it needs. Such a header should compile successfully when #included into a .cpp file by itself.
- Only #include what you need (don’t include everything just because you can).
- Do not #include .cpp files.
- Prefer putting documentation on what something does or how to use it in the header. It’s more likely to be seen there. Documentation describing how something works should remain in the source files.

[

Next lesson

2.12Header guards





](https://www.learncpp.com/cpp-tutorial/header-guards/)[

Back to table of contents





](https://www.learncpp.com/)[

Previous lesson

2.10Introduction to the preprocessor





](https://www.learncpp.com/cpp-tutorial/introduction-to-the-preprocessor/)


