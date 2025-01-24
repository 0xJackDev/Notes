
Header guards

The duplicate definition problem.

In lesson 2.7 we noted that a variable or function identifier can only have one definition. Thus a program that defines a variable identifier more then once will cause a compile error.


Similarly programs that define a function more then once will also cause a compile error 



While these programs are easy to fix (remove the duplicate definition), with header files, its quite easy too end up in a situation where a definition in a header file gets included into multiple .cpp files in a program.


Header Guards

The good news is that we can avoid the above problem via a mechanism called a header guard (also called an include guard). Header guards are conditional compilation directives that take the following form


#ifndef SOME_UNIQUE_NAME_HERE
#define SOME_UNIQUE_NAME_HERE

// your declarations (and certain types of definitions) here

#endif 




When this header is #included the preprocessor checks that "if not defined *funciton name*" has not been defined then it will define the function. If this header is included into the same file again since some_unique_name_here function has already been defined it will not be defined again

All of your header files should have header guards on them. _SOME_UNIQUE_NAME_HERE_ can be any name you want, but by convention is set to the full filename of the header file, typed in all caps, using underscores for spaces or punctuation. For example, _square.h_ would have the header guard:

#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

#endif 


Even the C++ standard library headers uses header guards. If you were to take a look at the iostream header file from visual studio, you would see 

#ifndef _IOSTREAM_
#define _IOSTREAM_

// content here

#endif 



Updating our previous example with header guards

Let’s return to the _square.h_ example, using the _square.h_ with header guards. For good form, we’ll also add header guards to _wave.h_.

square.h

```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

#endif
```

COPY

wave.h:

```cpp
#ifndef WAVE_H
#define WAVE_H

#include "square.h"

#endif
```

COPY

main.cpp:

```cpp
#include "square.h"
#include "wave.h"

int main()
{
    return 0;
}
```

COPY

After the preprocessor resolves all of the #include directives, this program looks like this:

main.cpp:
```cpp
// Square.h included from main.cpp
#ifndef SQUARE_H // square.h included from main.cpp
#define SQUARE_H // SQUARE_H gets defined here

// and all this content gets included
int getSquareSides()
{
    return 4;
}

#endif // SQUARE_H

#ifndef WAVE_H // wave.h included from main.cpp
#define WAVE_H
#ifndef SQUARE_H // square.h included from wave.h, SQUARE_H is already defined from above
#define SQUARE_H // so none of this content gets included

int getSquareSides()
{
    return 4;
}

#endif // SQUARE_H
#endif // WAVE_H

int main()
{
    return 0;
}
```



Header guards dont prevent a header from being included once into different code files

Note the goal of a header guard is to prevent code from receiving more then one copy of a guarded header. By design, header guards dont prevent a given header file from being included more then once into seperate code files which can cause seperate files consider the following:

square.h:

```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

int getSquarePerimeter(int sideLength); // forward declaration for getSquarePerimeter

#endif
```

COPY

square.cpp:

```cpp
#include "square.h"  // square.h is included once here

int getSquarePerimeter(int sideLength)
{
    return sideLength * getSquareSides();
}
```

COPY

main.cpp:

```cpp
#include "square.h" // square.h is also included once here
#include <iostream>

int main()
{
    std::cout << "a square has " << getSquareSides() << " sides\n";
    std::cout << "a square of length 5 has perimeter length " << getSquarePerimeter(5) << '\n';

    return 0;
}
```


Note that square.h is included from both main.cpp and square.cpp. This means the content of square.h will be included once into square.cpp and once into main.cpp

Lets examine why this happens in more detail. When square.h is included from square.cpp, SQUARE_H is defined until the end of square.cpp. This define prevents square.h from being included into square.cpp a second time( which is the point of header guards) however once square.cpp is finished SQUARE_H is no longer considered defined. This means when the preprocessor runs on main.cpp, Square_h is not initially defined in main.cpp.

The end result is that both square.cpp and main.cpp get a copy of the definition of getSquareSides. This program will compile bu the linker will complain about your program having multiple definitions of the identifer getSquareSides!

The best way to work around this issue is simply to put the function definition in one of the .cpp files so that the header just contains a forward declaration:


Generally we should avoid definitions in header files even with header guards

There are quite a few cases though where its necessary to put non-function definitions in a header file. For example C++ will let you create your own types. these custom types are typically defined in header files so the type definitons can be propagated out to the code files that need to use them. Without a header guard a code file could end up with multiple identical copies of a given definition which the compiler will flag as an error

#pragma once

Modern compiler support a simpler, alternate form of header guards using the #pragma preprocessor directive

```cpp
#pragma once

// your code here
```

`#pragma once` serves the same purpose as header guards: to avoid a header file from being included multiple times. With traditional header guards, the developer is responsible for guarding the header (by using preprocessor directives `#ifndef`, `#define`, and `#endif`). With `#pragma once`, we’re requesting that the compiler guard the header. How exactly it does this is an implementation-specific detail.


There is one known case where #pragma once will fail. If a header file is copied so that it exists in multiple places on the file system, if somehow both copies of the header get included, header guards will sucessfully de-dupe the identical headers but #pragma once wont (because the compiler wont realize they are actually identical)

most projects #pragma once is fine and most devs use it

he `#pragma` directive was designed for compiler implementers to use for whatever purposes they desire. As such, which pragmas are supported and what meaning those pragmas have is completely implementation-specific. With the exception of `#pragma once`, do not expect a pragma that works on one compiler to be supported by another.


Because `#pragma once` is not defined by the C++ standard, it is possible that some compilers may not implement it. For this reason, some development houses (such as Google) recommend using traditional header guards. In this tutorial series, we will favor header guards, as they are the most conventional way to guard headers. However, support for `#pragma once` is fairly ubiquitous at this point, and if you wish to use `#pragma once` instead, that is generally accepted in modern C++.




SUMMARY:

Header guards are desgined to ensure that the contents of a given header file are not copied more than once into a single file.
