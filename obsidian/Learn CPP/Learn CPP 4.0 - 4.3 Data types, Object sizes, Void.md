

Each BYTE inside of memory has its own memory address. 


| Types                                                                              | Category             | Meaning                                          | Example |
| ---------------------------------------------------------------------------------- | -------------------- | ------------------------------------------------ | ------- |
| float  <br>double  <br>long double                                                 | Floating Point       | a number with a fractional part                  | 3.14159 |
| bool                                                                               | Integral (Boolean)   | true or false                                    | true    |
| char  <br>wchar_t  <br>char8_t (C++20)  <br>char16_t (C++11)  <br>char32_t (C++11) | Integral (Character) | a single character of text                       | ‘c’     |
| short int  <br>int  <br>long int  <br>long long int (C++11)                        | Integral (Integer)   | positive and negative whole numbers, including 0 | 64      |
| std::nullptr_t (C++11)                                                             | Null Pointer         | a null pointer                                   | nullptr |
| void                                                                               | Void                 | no type                                          | n/a     |

This chapter is dedicated to exploring these fundamental data types in detail (except std::nullptr_t, which we’ll discuss when we talk about pointers). C++ also supports a number of other more complex types, called _compound types_. We’ll explore compound types in a future chapter.



In mathematics, an _integer_ is a number with no decimal or fractional part, including negative and positive numbers and zero.


The term _integral_ means “like an integer”. Most often, _integral_ is used as part of the term “integral type”, which includes the broader set of types that are stored in memory as integers, even though their behaviors might vary (which we’ll see later in this chapter when we talk about the character types). This includes `bool`, the integer types, and all the various character types.




Most modern programming languages include a fundamental `string` type (strings are a data type that lets us hold a sequence of characters, typically used to represent text). In C++, strings aren’t a fundamental type (they’re a compound type). But because basic string usage is straightforward and useful, we’ll introduce strings in the next chapter (in lesson [5.9 -- Introduction to std::string](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring/)).



4.2


Void is our first example of an incomplete type. An **incomplete type** is a type that has been declared but not yet defined. The compiler knows about the existence of such types, but does not have enough information to determine how much memory to allocate for objects of that type. `void` is intentionally incomplete since it represents the lack of a type, and thus cannot be defined.


for example this wont work
void value; // Wont work since Variables cant be defined with an incomplete type voids





Although void is really useful if you want a function that doesnt return a value. For example prints something to the screen you can set the return type of void, and no return is expected.


#include <iostream>


void print() {
	std::cout << "Hello" << std::endl;
}

int main() {
	print();
}

for example.


Also in C++ single quotes identify a single char like 'a' while double quotes create an string which is an array of chars. for example "String" but these are not used interchangeably 





4.3


However, this analogy is not quite correct in one regard -- most objects actually take up more than 1 byte of memory. A single object may use 1, 2, 4, 8, or even more consecutive memory addresses. The amount of memory that an object uses is based on its data type.


To generalize, an object with _n_ bits (where n is an integer) can hold 2n (2 to the power of n, also commonly written 2^n) unique values. Therefore, with an 8-bit byte, a byte-sized object can hold 28 (256) different values. An object that uses 2 bytes can hold 2^16 (65536) different values!

Thus, the size of the object puts a limit on the amount of unique values it can store -- objects that utilize more bytes can store a larger number of unique values. We will explore this further when we talk more about integers.

New programmers often focus too much on optimizing their code to use as little memory as possible. In most cases, this makes a negligible difference. Focus on writing maintainable code, and optimize only when and where the benefit will be substantive.


The obvious next question is “how much memory do variables of different data types take?”.

Perhaps surprisingly, the C++ standard does not define the exact size (in bits) for any of the fundamental types. char must be 1 byte, but no assumption is made that a byte is 8 bits. Integral types have a minimum size (in bits), but could be larger.

In this tutorial series, we will take a simplified view, by making some reasonable assumptions that are generally true for modern architectures:

- A byte is 8 bits.
- Memory is byte addressable, so the smallest object is 1 byte.
- Floating point support is IEEE-754 compliant.
- We are on a 32-bit or 64-bit architecture.

Given that, we can state the following:




|Category|Type|Minimum Size|Typical Size|Note|
|---|---|---|---|---|
|Boolean|bool|1 byte|1 byte||
|character|char|1 byte|1 byte|always exactly 1 byte|
||wchar_t|1 byte|2 or 4 bytes||
||char8_t|1 byte|1 byte||
||char16_t|2 bytes|2 bytes||
||char32_t|4 bytes|4 bytes||
|integer|short|2 bytes|2 bytes||
||int|2 bytes|4 bytes||
||long|4 bytes|4 or 8 bytes||
||long long|8 bytes|8 bytes||
|floating point|float|4 bytes|4 bytes||
||double|8 bytes|8 bytes||
||long double|8 bytes|8, 12, or 16 bytes||
|pointer|std::nullptr_t|4 bytes|4 or 8 bytes||

  



In order to determine the size of data types on a particular machine, C++ provides an operator named _sizeof_. The **sizeof operator** is a unary operator that takes either a type or a variable, and returns its size in bytes. You can compile and run the following program to find out how large some of your data types are:



#include <iomanip> // for std::setw (which sets the width of the subsequent output)
#include <iostream>

int main()
{
    std::cout << std::left; // left justify output
    std::cout << std::setw(16) << "bool:" << sizeof(bool) << " bytes\n";
    std::cout << std::setw(16) << "char:" << sizeof(char) << " bytes\n";
    std::cout << std::setw(16) << "short:" << sizeof(short) << " bytes\n";
    std::cout << std::setw(16) << "int:" << sizeof(int) << " bytes\n";
    std::cout << std::setw(16) << "long:" << sizeof(long) << " bytes\n";
    std::cout << std::setw(16) << "long long:" << sizeof(long long) << " bytes\n";
    std::cout << std::setw(16) << "float:" << sizeof(float) << " bytes\n";
    std::cout << std::setw(16) << "double:" << sizeof(double) << " bytes\n";
    std::cout << std::setw(16) << "long double:" << sizeof(long double) << " bytes\n";

    return 0;
}

bool:           1 bytes
char:           1 bytes
short:          2 bytes
int:            4 bytes
long:           4 bytes
long long:      8 bytes
float:          4 bytes
double:         8 bytes
long double:    8 bytes





Trying to use `sizeof` on an incomplete type (such as `void`) will result in a compilation error.

You can also use the `sizeof` operator on a variable name:
for example

#include <iostream>

int main()
{
    int x{};
    std::cout << "x is " << sizeof(x) << " bytes\n";

    return 0;
}


returns x is four bytes

`sizeof` does not include dynamically allocated memory used by an object. We discuss dynamic memory allocation in a future lesson.