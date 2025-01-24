introduction to the preprocessor

When you compile your project you might expect that the compiler compiles each code file exactly as you've written it this isn't actually the case.

Instead prior to compilation, each .cpp file goes through a preprocessing phase. In this phase a program called the preprocessor makes various changes to the text of the code file. The preprocessor does not modify the original code files in any way -- rather all changes made by the preprocessor happen either temporarily in memory or using temporary files.

Most of what the preprocessor does is pretty uninteresting, it strips out comments and ensure each code file ends in a newline. However the preprcessor does have one important rule: it is what processes the #include directives

When the preprocessor has finished processing a code file the result is called a translation unit. This translation unit is what is compiled by the compiler

The entire process of preprocessing, compiling, and linking is called translation 

Preprocessor directives are often just called directives and they are instruction that start with the # symbol and end with a newline NOT A SEMICOLON. These directives tell the preprocessor to perform certain text manipulation tasks. Note that the preprocessor does not understand C++ syntax instead the directives have their own syntax

#include.

youve already seen the #include directive in action to #include <iostream> when you #include a file. The preprocessor replaces the #include directive with the contents of the included file. The included contents are then preprocessed which may result in more #include statements and then the rest of the file is preprocessing, Basically in simple terms #include just copy's all the code from the file you are including into the source file you typed #include into

Once the preprocessor has finished processing the code file plus all of the #included content the result is called a translation unit. The translation unit is what is then sent to the compiler to be compiled

A translation unit contains both the processed code from the code file as well as the processed code from all of the #included files

#include is almost exclusively used to include header files


Macro defines

The #define directive can be used to create a macro. In C++
a macro is a rule that defines how input text is converted into replacement output text.

There are two basic types of macros: *object-like macros* and *function-like macros*

Function-like macros act like functions and serve a similar purpose. Their use is generally considered unsafe and bad practice almost anything that they do can be done with normal functions.

Object-like macros can be defined in one of two ways

#define identifier
#define identifier substitution_text

The top definition has no substitution text, whereas the bottom one does. Because these are preprocessor directives and not statements they do not end with ;

The identifier for a macro uses the same naming rules as normal identifier: they can use numbers, letters, and underscores, cannot start with a number and shouldn't start with an underscore. By convention macro names are typically all upercase seperated by underscores

Object-like macros with substitution text

When the preprocessor encounters this directive any further occurrence of the identifier is replaced by subsitution_text. The identifier is traditionally typed in all capital letter

consider the program

#include <iostream>

#define MY_NAME "Alex"

int main()
{
    std::cout << "My name is: " << MY_NAME << '\n';

    return 0;
}


The preprocessor will replace MY_NAME with "Alex". *note that the replacement doesn't have to use "" but since we are replacing it with a string thats why we are* 

When run will output My name is: alex

Usually this is only seen in legacy code We avoid using macros now in modern coding standard


Object-like macros without substitution text.

for example
#define USE_YEN

Macros like this would work as you expect, any further occurence of this identifier is just removed and replaced by nothing so really there is only one type of object-like macros cause it either replaces it with something or just deletes it entirely if no replacement is supplied. However these forms are generally considered good practice in C++ and is seen alot


Conditional compilation

The conditional compilation preprocessor directives allow you to specify under what conditions something will or wont compile. There are quite a few different conditional compilation directives but the main three are #ifdef, #ifndef, and #endef.

the #indef preprocessor directive allows the preprocessor to check whether an identifier has been previously #defined. if so the code between the #ifdef and #endif is compiled. If not the code is ignored. Consider the code below 

#include <iostream>

#define PRINT_JOE

int main()
{
#ifdef PRINT_JOE
    std::cout << "Joe\n"; // will be compiled since PRINT_JOE is defined
#endif

#ifdef PRINT_BOB
    std::cout << "Bob\n"; // will be excluded since PRINT_BOB is not defined
#endif

    return 0;
}

In this code since we #define PRINT_JOE The console will output Joe and run all the code between the beginning of #ifdef to #endif
But since PRINT_BOB wasn't defined the code is ignored 

#ifndef is the opposite of #ifdef it allows you to check whether the identfier has not been defined yet 

#endif ends it for both.

Consider the following code 

#include <iostream>

int main()
{
#ifndef PRINT_BOB
    std::cout << "Bob\n";
#endif

    return 0;
}

since #define PRINT_BOB is not defined the code is ran and Bob is printed to teh console


In place of `#ifdef PRINT_BOB` and `#ifndef PRINT_BOB`, you’ll also see `#if defined(PRINT_BOB)` and `#if !defined(PRINT_BOB)`. These do the same, but use a slightly more C++-style syntax.




One more common use of conditional compilation involves using #if 0 to exclude a block of code form being compiled as if it were inside a comment block consider the following

#include <iostream>

int main()
{
    std::cout << "Joe\n";

#if 0 // Don't compile anything starting here
    std::cout << "Bob\n";
    std::cout << "Steve\n";
#endif // until this point

    return 0;
}

To temporarily re enable code that is been wrapped in an #if 0 you can change it to #if 1 and it will run


Object-like macros dont affect other preprocessor directives

Consider the following

#define PRINT_JOE

#ifdef PRINT_JOE
// ...


since we defined PRINT_JOE to be replaced by nothign how come that preprocessor #ifdef PRINT_JOE didnt replace PRINT_JOE with nothing?

Macros only cause text substitution for non-preprocessor commands 

the scope of #defines 

Directives are resolved before compilation from a top to bottom on a file by file basis.

Once the preprocessor has finished, all defined identifiers from that file are discarded. This means that directives are only valid from the point of definition to the end of the file in which they are defined. Directives defined in one code file do not have impact on other code files in the same project.


Consider the following example:

function.cpp:

```cpp
#include <iostream>

void doSomething()
{
#ifdef PRINT
    std::cout << "Printing!\n";
#endif
#ifndef PRINT
    std::cout << "Not printing!\n";
#endif
}
```

COPY

main.cpp:

```cpp
void doSomething(); // forward declaration for function doSomething()

#define PRINT

int main()
{
    doSomething();

    return 0;
}
```


The above program will print.
Not printing!

Even though PRINT was defined in main.cpp that doesnt have any impact on any code in the funciton.cpp (PRINT IS ONLY #defined) from the point of definition to the end of main.cpp

