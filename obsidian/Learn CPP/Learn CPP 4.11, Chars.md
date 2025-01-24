

The **char** data type was designed to hold a single `character`. A **character** can be a single letter, number, symbol, or whitespace.


The char data type is an integral type, meaning the underlying value is stored as an integer. Similar to how a Boolean value `0` is interpreted as `false` and non-zero is interpreted as `true`, the integer stored by a `char` variable are intepreted as an `ASCII character`.

**ASCII** stands for American Standard Code for Information Interchange, and it defines a particular way to represent English characters (plus a few other symbols) as numbers between 0 and 127 (called an **ASCII code** or **code point**). For example, ASCII code 97 is interpreted as the character ‘a’.

Character literals are always placed between single quotes (e.g. ‘g’, ‘1’, ‘ ‘).

Here’s a full table of ASCII characters:


Initializing chars

You can initialize char variables using character literals:

```cpp
char ch2{ 'a' }; // initialize with code point for 'a' (stored as integer 97) (preferred)
```

Copy

You can initialize chars with integers as well, but this should be avoided if possible

```cpp
char ch1{ 97 }; // initialize with integer 97 ('a') (not preferred)
```



Warning

Be careful not to mix up character numbers with integer numbers. The following two initializations are not the same:

```cpp
char ch{5}; // initialize with integer 5 (stored as integer 5)
char ch{'5'}; // initialize with code point for '5' (stored as integer 53)
```

Copy

Character numbers are intended to be used when we want to represent numbers as text, rather than as numbers to apply mathematical operations to.



BREAK 

```
#include <iostream>


int main() {
	std::string x{ "hello" };
	char b{ 'h' };

	std::cout << x << '\n';
	std::cout << b << '\n';

}
```

As you can see i had to use the data type std::string from the standard library this is because unlike chars, strings are not an inheritly defined data type in C++ instead a string is actually just an array of Chars.



Note that std::cin will let you enter multiple characters. However, variable _ch_ can only hold 1 character. Consequently, only the first input character is extracted into variable _ch_. The rest of the user input is left in the input buffer that std::cin uses, and can be extracted with subsequent calls to std::cin.

You can see this behavior in the following example:

```cpp
#include <iostream>

int main()
{
    std::cout << "Input a keyboard character: "; // assume the user enters "abcd" (without quotes)

    char ch{};
    std::cin >> ch; // ch = 'a', "bcd" is left queued.
    std::cout << "You entered: " << ch << '\n';

    // Note: The following cin doesn't ask the user for input, it grabs queued input!
    std::cin >> ch; // ch = 'b', "cd" is left queued.
    std::cout << "You entered: " << ch << '\n';

    return 0;
}
```

Copy

Input a keyboard character: abcd
You entered: a
You entered: b


Input a keyboard character: abcd
You entered: a
You entered: b


If you want to read in more than one char at a time (e.g. to read in a name, word, or sentence), you’ll want to use a string instead of a char. A string is a collection of sequential characters (and thus, a string can hold multiple symbols). We discuss this in upcoming lesson ([5.9 -- Introduction to std::string](https://www.learncpp.com/cpp-tutorial/introduction-to-stdstring/)).



Char size, range, and default sign

Char is defined by C++ to always be 1 byte in size. By default, a char may be signed or unsigned (though it’s usually signed). If you’re using chars to hold ASCII characters, you don’t need to specify a sign (since both signed and unsigned chars can hold values between 0 and 127).

If you’re using a char to hold small integers (something you should not do unless you’re explicitly optimizing for space), you should always specify whether it is signed or unsigned. A signed char can hold a number between -128 and 127. An unsigned char can hold a number between 0 and 255.


Escape sequences

There are some sequences of characters in C++ that have special meaning. These characters are called **escape sequences**. An escape sequence starts with a ‘\’ (backslash) character, and then a following letter or number.

You’ve already seen the most common escape sequence: `'\n'`, which can be used to print a newline:

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    std::cout << "The value of x is: " << x << '\n'; // standalone \n goes in single quotes
    std::cout << "First line\nSecond line\n";        // \n can be embedded in double quotes
    return 0;
}
```

Copy

This outputs:

The value of x is: 5
First line
Second line

Another commonly used escape sequence is `'\t'`, which embeds a horizontal tab:

```cpp
#include <iostream>

int main()
{
    std::cout << "First part\tSecond part";
    return 0;
}
```

Copy

Which outputs:

First part	Second part

Three other notable escape sequences are:  
\’ prints a single quote  
\” prints a double quote  
\\ prints a backslash

Here’s a table of all of the escape sequences:

|Name|Symbol|Meaning|
|---|---|---|
|Alert|\a|Makes an alert, such as a beep|
|Backspace|\b|Moves the cursor back one space|
|Formfeed|\f|Moves the cursor to next logical page|
|Newline|\n|Moves cursor to next line|
|Carriage return|\r|Moves cursor to beginning of line|
|Horizontal tab|\t|Prints a horizontal tab|
|Vertical tab|\v|Prints a vertical tab|
|Single quote|\’|Prints a single quote|
|Double quote|\”|Prints a double quote|
|Backslash|\\|Prints a backslash.|
|Question mark|\?|Prints a question mark.  <br>No longer relevant. You can use question marks unescaped.|
|Octal number|\(number)|Translates into char represented by octal|
|Hex number|\x(number)|Translates into char represented by hex number|



Warning

Escape sequences start with a backslash (\), not a forward slash (/). If you use a forward slash by accident, it may still compile, but will not yield the desired result.


What’s the difference between putting symbols in single and double quotes?

Text between single quotes is treated as a `char` literal, which represents a single character. For example, `'a'` represents the character `a`, `'+'` represents the character for the plus symbol, `'5'` represents the character `5` (not the number 5), and `'\n'` represents the newline character.

Text between double quotes (e.g. “Hello, world!”) is treated as a C-style string literal, which can contain multiple characters. We discuss strings in lesson [5.2 -- Literals](https://www.learncpp.com/cpp-tutorial/literals/).

Best practice

Single characters should usually be single-quoted, not double-quoted (e.g. `'t'` or `'\n'`, not `"t"` or `"\n"`). One possible exception occurs when doing output, where it can be preferential to double quote everything for consistency (see lesson [1.5 -- Introduction to iostream: cout, cin, and endl](https://www.learncpp.com/cpp-tutorial/introduction-to-iostream-cout-cin-and-endl/)).

Avoid multicharacter literals

For backwards compatibility reasons, many C++ compilers support **multicharacter literals**, which are char literals that contain multiple characters (e.g. `'56'`). If supported, these have an implementation-defined value (meaning it varies depending on the compiler). Because they are not part of the C++ standard, and their value is not strictly defined, multicharacter literals should be avoided.

Best practice

Avoid multicharacter literals (e.g. `'56'`).

Multicharacter literal support sometimes causes problems for new programmers. Consider the following simple program:

```cpp
#include <iostream>

int add(int x, int y)
{
	return x + y;
}

int main()
{
	std::cout << add(1, 2) << '/n';

	return 0;
}
```

Copy

The programmer expects this program to print the value `3` and a newline. But instead, on the author’s machine, it outputs the following:

312142

The issue here is that the programmer accidentally used `'/n'` (a multicharacter literal consisting of a forward slash and an `'n'` character) instead of `'\n'` (the escape sequence for a newline). The program first prints `3` (the result of `add(1, 2)`) correctly. But then it prints the value of `'/n'`, which on the author’s machine had the implementation-defined value `12142`.


But this output isn’t nearly exciting enough, so we decide to add an exclamation point before the newline:

```cpp
#include <iostream>

int main()
{
    int x { 5 };
    std::cout << "The value of x is " << x << '!\n'; // added exclamation point

    return 0;
}
```

Copy

Because `'!\n'` is a multicharacter literal, this program now prints:

The value of x is 58458


What about the other char types, `wchar_t`, `char8_t`, `char16_t`, and `char32_t`?

`wchar_t` should be avoided in almost all cases (except when interfacing with the Windows API). Its size is implementation defined, and is not reliable. It has largely been deprecated.

As an aside…

The term “deprecated” means “still supported, but no longer recommended for use, because it has been replaced by something better or is no longer considered safe”.


Much like ASCII maps the integers 0-127 to American English characters, other character encoding standards exist to map integers (of varying sizes) to characters in other languages. The most well-known mapping outside of ASCII is the Unicode standard, which maps over 144,000 integers to characters in many different languages. Because Unicode contains so many code points, a single Unicode code point needs 32-bits to represent a character (called UTF-32). However, Unicode characters can also be encoded using multiple 16-bit or 8-bit characters (called UTF-16 and UTF-8 respectively).

`char16_t` and `char32_t` were added to C++11 to provide explicit support for 16-bit and 32-bit Unicode characters. These char types have the same size as `std::uint_least16_t` and `std::uint_least32_t` respectively (but are distinct types). `char8_t` was added in C++20 to provide support for 8-bit Unicode (UTF-8). It is a distinct type that uses the same representation as `unsigned char`.

You won’t need to use `char8_t`, `char16_t`, or `char32_t` unless you’re planning on making your program Unicode compatible. Unicode and localization are generally outside the scope of these tutorials, so we won’t cover it further.




