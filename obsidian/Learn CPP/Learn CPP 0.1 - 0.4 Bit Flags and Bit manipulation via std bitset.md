

On modern computer architectures, the smallest addressable unit of memory is a byte. Since all objects need to have unique memory addresses, this means objects must be at least one byte in size. For most variable types, this is fine. However, for Boolean values, this is a bit wasteful (pun intended). Boolean types only have two states: true (1), or false (0). This set of states only requires one bit to store. However, if a variable must be at least a byte, and a byte is 8 bits, that means a Boolean is using 1 bit and leaving the other 7 unused.


In the majority of cases, this is fine -- we’re usually not so hard-up for memory that we need to care about 7 wasted bits (we’re better off optimizing for understandability and maintainability). However, in some storage-intensive cases, it can be useful to “pack” 8 individual Boolean values into a single byte for storage efficiency purposes.


Doing these things requires that we can manipulate objects at the bit level. Fortunately, C++ gives us tools to do precisely this. Modifying individual bits within an object is called **bit manipulation**.




However, instead of viewing objects as holding a single value, we can instead view them as a collection of individual bits. When individual bits of an object are used as Boolean values, the bits are called **bit flags**.


To define a set of bit flags, we’ll typically use an unsigned integer of the appropriate size (8 bits, 16 bits, 32 bits, etc… depending on how many flags we have), or std::bitset.

```cpp
#include <bitset> // for std::bitset

std::bitset<8> mybitset {}; // 8 bits in size means room for 8 flags
```


Bit numbering and bit positions

Given a sequence of bits, we typically number the bits from right to left, starting with 0 (not 1). Each number denotes a **bit position**.

76543210  Bit position
00000101  Bit sequence

Given the bit sequence 0000 0101, the bits that are in position 0 and 2 have value 1, and the other bits have value 0.



Manipulating bits via std::bitset

In lesson [5.3 -- Numeral systems (decimal, binary, hexadecimal, and octal)](https://www.learncpp.com/cpp-tutorial/numeral-systems-decimal-binary-hexadecimal-and-octal/) we already showed how to use a std::bitset to print values in binary. However, this isn’t the only useful thing std::bitset can do.

std::bitset provides 4 key member functions that are useful for doing bit manipulation:

- test() allows us to query whether a bit is a 0 or 1.
- set() allows us to turn a bit on (this will do nothing if the bit is already on).
- reset() allows us to turn a bit off (this will do nothing if the bit is already off).
- flip() allows us to flip a bit value from a 0 to a 1 or vice versa.

Each of these functions takes the position of the bit we want to operate on as their only argument.

Here’s an example:

```cpp
#include <bitset>
#include <iostream>

int main()
{
    std::bitset<8> bits{ 0b0000'0101 }; // we need 8 bits, start with bit pattern 0000 0101
    bits.set(3);   // set bit position 3 to 1 (now we have 0000 1101)
    bits.flip(4);  // flip bit 4 (now we have 0001 1101)
    bits.reset(4); // set bit 4 back to 0 (now we have 0000 1101)

    std::cout << "All the bits: " << bits<< '\n';
    std::cout << "Bit 3 has value: " << bits.test(3) << '\n';
    std::cout << "Bit 4 has value: " << bits.test(4) << '\n';

    return 0;
}
```

Copy

This prints:

All the bits: 00001101
Bit 3 has value: 1
Bit 4 has value: 0


The bitwise operators

C++ provides 6 bit manipulation operators, often called **bitwise** operators:

|Operator|Symbol|Form|Operation|
|---|---|---|---|
|left shift|<<|x << y|all bits in x shifted left y bits|
|right shift|>>|x >> y|all bits in x shifted right y bits|
|bitwise NOT|~|~x|all bits in x flipped|
|bitwise AND|&|x & y|each bit in x AND each bit in y|
|bitwise OR|\||x \| y|each bit in x OR each bit in y|
|bitwise XOR|^|x ^ y|each bit in x XOR each bit in y|



Bitwise left shift (<<) and bitwise right shift (>>) operators

The **bitwise left shift** (<<) operator shifts bits to the left. The left operand is the expression to shift the bits of, and the right operand is an integer number of bits to shift left by.

So when we say `x << 1`, we are saying “shift the bits in the variable x left by 1 place”. New bits shifted in from the right side receive the value 0.

0011 << 1 is 0110  
0011 << 2 is 1100  
0011 << 3 is 1000

Note that in the third case, we shifted a bit off the end of the number! Bits that are shifted off the end of the binary number are lost forever.

The **bitwise right shift** (>>) operator shifts bits to the right.

1100 >> 1 is 0110  
1100 >> 2 is 0011  
1100 >> 3 is 0001

Note that in the third case we shifted a bit off the right end of the number, so it is lost.

Here’s an example of doing some bit shifting:

```cpp
#include <bitset>
#include <iostream>

int main()
{
    std::bitset<4> x { 0b1100 };

    std::cout << x << '\n';
    std::cout << (x >> 1) << '\n'; // shift right by 1, yielding 0110
    std::cout << (x << 1) << '\n'; // shift left by 1, yielding 1000

    return 0;
}
```

Copy

This prints:

1100
0110
1000


What!? Aren’t operator<< and operator>> used for input and output?

They sure are.

Programs today typically do not make much use of the bitwise left and right shift operators to shift bits. Rather, you tend to see the bitwise left shift operator used with std::cout (or other stream objects) to output text. Consider the following program:

```cpp
#include <bitset>
#include <iostream>

int main()
{
    unsigned int x { 0b0100 };
    x = x << 1; // use operator<< for left shift
    std::cout << std::bitset<4>{ x } << '\n'; // use operator<< for output

    return 0;
}
```

Copy

This program prints:

1000

In the above program, how does operator<< know to shift bits in one case and output _x_ in another case? The answer is that std::cout has **overloaded** (provided an alternate definition for) operator<< that does console output rather than bit shifting.

When the compiler sees that the left operand of operator<< is std::cout, it knows that it should call the version of operator<< that std::cout overloaded to do output. If the left operand is an integral type, then operator<< knows it should do its usual bit-shifting behavior.

The same applies for operator>>.

Note that if you’re using operator << for both output and left shift, parenthesization is required:

```cpp
#include <bitset>
#include <iostream>

int main()
{
	std::bitset<4> x{ 0b0110 };

	std::cout << x << 1 << '\n'; // print value of x (0110), then 1
	std::cout << (x << 1) << '\n'; // print x left shifted by 1 (1100)

	return 0;
}
```

Copy

This prints:

01101
1100

The first line prints the value of x (0110), and then the literal 1. The second line prints the value of x left-shifted by 1 (1100).

We will talk more about operator overloading in a future chapter, including discussion of how to overload operators for your own purposes.

Bitwise NOT

The **bitwise NOT** operator (~) is perhaps the easiest to understand of all the bitwise operators. It simply flips each bit from a 0 to a 1, or vice versa. Note that the result of a _bitwise NOT_ is dependent on what size your data type is.

Flipping 4 bits:  
~0100 is 1011

Flipping 8 bits:  
~0000 0100 is 1111 1011

In both the 4-bit and 8-bit cases, we start with the same number (binary 0100 is the same as 0000 0100 in the same way that decimal 7 is the same as 07), but we end up with a different result.

We can see this in action in the following program:

```cpp
#include <bitset>
#include <iostream>

int main()
{
	std::cout << ~std::bitset<4>{ 0b0100 } << ' ' << ~std::bitset<8>{ 0b0100 } << '\n';

	return 0;
}
```

Copy

This prints:  
1011 11111011


Lesson 0.3
https://www.learncpp.com/cpp-tutorial/bit-manipulation-with-bitwise-operators-and-bit-masks/


Summary

Summarizing how to set, clear, toggle, and query bit flags:

To query bit states, we use _bitwise AND_:

```cpp
if (flags & option4) ... // if option4 is set, do something
```

Copy

To set bits (turn on), we use _bitwise OR_:

```cpp
flags |= option4; // turn option 4 on.
flags |= (option4 | option5); // turn options 4 and 5 on.
```

Copy

To clear bits (turn off), we use _bitwise AND_ with _bitwise NOT_:

```cpp
flags &= ~option4; // turn option 4 off
flags &= ~(option4 | option5); // turn options 4 and 5 off
```

Copy

To flip bit states, we use _bitwise XOR_:

```cpp
flags ^= option4; // flip option4 from on to off, or vice versa
flags ^= (option4 | option5); // flip options 4 and 5
```



0.4 https://www.learncpp.com/cpp-tutorial/converting-integers-between-binary-and-decimal-representation/

 O.4 — Converting integers between binary and decimal representation
