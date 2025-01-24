

A syntax error occurs when you write a statement that is not according to the grammar of the C++ language. The compiler will identify these problems though for example missing a semicolon at the end of a line is an example of a syntax error



Once you get your program compiling right getting the results you want can be tricky. A semantic error occurs when a statement is syntactically valid but doesn't do what the programmer intended.

Sometimes these will cause your programs to crash as is the case if you try to divide by 0

#include <iostream>

int main()
{
    int a { 10 };
    int b { 0 };
    std::cout << a << " / " << b << " = " << a / b << '\n'; // division by 0 is undefined in mathematics
    return 0;
}

More often these will just produce wrong value or wrong behavior 
#include <iostream>

int main()
{
    int x; // no initializer provided
    std::cout << x << '\n'; // Use of uninitialized variable leads to undefined result

    return 0;
}


Or 

say you put a + instead of a - that would be a semantic error


Modern compilers have been getting better at detecting certain types of common semantic errors (e.g. use of an uninitialized variable). However, in most cases, the compiler will not be able to catch most of these types of problems, because the compiler is designed to enforce grammar, not intent.