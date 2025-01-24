

4.4 Signed Integer

An integer is a integral type that can represent positive and negative numbers. There are 4 fundamental integer types available for use. 


| Type          | Min-size | Notes                                     |
| ------------- | -------- | ----------------------------------------- |
| short int     | 16 bits  |                                           |
|               |          |                                           |
| int           | 16 bits  | Typically 32 bits on modern architectures |
|               |          |                                           |
|               |          |                                           |
| long int      | 32 bits  |                                           |
|               |          |                                           |
| long long int | 64 bits  |                                           |
The key difference between the various integer types is that they have varying sizes -- the larger integers can hold bigger numbers.


Technically, the `bool` and `char` types are considered to be integral types (because these types store their values as integer values). For the purpose of the next few lessons, we’ll exclude these types from our discussion.


Signed integers

When writing negative numbers in everyday life, we use a negative sign. For example, _-3_ means “negative 3”. We’d also typically recognize _+3_ as “positive 3” (though common convention dictates that we typically omit plus prefixes).

This attribute of being positive, negative, or zero is called the number’s **sign**.

By default, integers in C++ are **signed**, which means the number’s sign is stored as part of the value. Therefore, a signed integer can hold both positive and negative numbers (and 0).

In this lesson, we’ll focus on signed integers. We’ll discuss unsigned integers (which can only hold non-negative numbers) in the next lesson.


Defining signed integers

Here is the preferred way to define the four types of signed integers:

```cpp
short s;      // prefer "short" instead of "short int"
int i;
long l;       // prefer "long" instead of "long int"
long long ll; // prefer "long long" instead of "long long int"
```



Although _short int_, _long int_, or _long long int_ will work, we prefer the short names for these types (that do not use the _int_ suffix). In addition to being more typing, adding the _int_ suffix makes the type harder to distinguish from variables of type _int_. This can lead to mistakes if the short or long modifier is inadvertently missed.

The integer types can also take an optional _signed_ keyword, which by convention is typically placed before the type name:

However, this keyword should not be used, as it is redundant, since integers are signed by default.


Here’s a table containing the range of signed integers of different sizes:


| Size/Type     | Range                                                   |
| ------------- | ------------------------------------------------------- |
| 8 bit signed  | -128 to 127                                             |
|               |                                                         |
| 16 bit signed | -32,768 to 32,767                                       |
|               |                                                         |
| 32 bit signed | -2,147,483,648 to 2,147,483,647                         |
|               |                                                         |
| 64 bit signed | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |


If we try to assign a larger value then one of these singed integers can hold then we get a overflow. 
The C++20 standard makes this blanket statement: “If during the evaluation of an expression, the result is not mathematically defined or not in the range of representable values for its type, the behavior is undefined”. Colloquially, this is called **overflow**.

This results in undefined behavior. 


We cover what happens when unsigned integers overflow in lesson [4.5 -- Unsigned integers, and why to avoid them](https://www.learncpp.com/cpp-tutorial/unsigned-integers-and-why-to-avoid-them/).


When dividing two integers, C++ works like you’d expect when the quotient is a whole number:

```cpp
#include <iostream>

int main()
{
    std::cout << 20 / 4 << '\n';
    return 0;
}
```

Copy

This produces the expected result:

5

But let’s look at what happens when integer division causes a fractional result:

```cpp
#include <iostream>

int main()
{
    std::cout << 8 / 5 << '\n';
    return 0;
}
```

Copy

This produces a possibly unexpected result:

1


When doing division with two integers (called **integer division**), C++ always produces an integer result. Since integers can’t hold fractional values, any fractional portion is simply dropped (not rounded!).


2





4.5 Unsigned Integers


Unsigned integers are integers that can only hold non-negative numbers


To define a an unsigned integer we use the unsigned keyword. By convention this is placed before the type for example say you wannt declare an unsigned long 


unsigned long;


Since these Dont have negative numbers you are able to store a much larger Integer value.



| Size/type       | Range of numbers possible       |
| --------------- | ------------------------------- |
| 8 bit unsigned  | 0 to 255                        |
| 16 bit unsigned | 0 to 65,535                     |
| 32 bit unsigned | 0 to 4,294,967,295              |
| 64 bit unsigned | 0 to 18,446,744,073,709,551,615 |



Unsigned Integer Overflow


So what happens if we try to store the number 280 inside of a 8 bit unsigned integer. The answer is overflow.




## AUTHORS NOTE

	Oddly the C++ standard explicity says "a computation involving unsigned operands can never overflow" this is contrary to general programming consesus though because integer overflow encompasses signed and unsigned use cases. Given most programmers consider this We will call this an overflow despite the Author of C++ not wanting to admit that hes a fuckhead




If an unsigned value is out of range it is divided by one greater than the largest number of the type and only the reminder is kept.


Going back to putting the value of 280 inside of the 8 bit unsigned integer since 280 is too large to fit in our 1-byte range of 0-255. 1 greater than the largest number of this type is 256. therefor we divide 280 by 256 getting 1 with the reminder of 24. The remainder 24 is what is stored. Weird right?


Here’s another way to think about the same thing. Any number bigger than the largest number representable by the type simply “wraps around” (sometimes called “modulo wrapping”). `255` is in range of a 1-byte integer, so `255` is fine. `256`, however, is outside the range, so it wraps around to the value `0`. `257` wraps around to the value `1`. `280` wraps around to the value `24`.



Consider the following program which represents this using a 16-bit unsigned values

```

#include <iostream>

int main()
{
    unsigned short x{ 65535 }; // largest 16-bit unsigned value possible
    std::cout << "x was: " << x << '\n';

    x = 65536; // 65536 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    x = 65537; // 65537 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    return 0;
}
```

This would return 

x was: 65535
x is now: 0
x is now: 1


The reason the second one is 0 is because we aren't actually dividing the value wraps around to 0 because 65536 is exactly one more than the max value of the unsigned short can hold, effectivley resetting its range to 0 


    x = 65540; // 65537 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

if i changed it to this. Then it would then print 4.




Alot of times this is where bugs in video games occur

It’s possible to wrap around the other direction as well. 0 is representable in a 2-byte unsigned integer, so that’s fine. -1 is not representable, so it wraps around to the top of the range, producing the value 65535. -2 wraps around to 65534. And so forth.

```cpp
#include <iostream>

int main()
{
    unsigned short x{ 0 }; // smallest 2-byte unsigned value possible
    std::cout << "x was: " << x << '\n';

    x = -1; // -1 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    x = -2; // -2 is out of our range, so we get modulo wrap-around
    std::cout << "x is now: " << x << '\n';

    return 0;
}
```



x was: 0
x is now: 65535
x is now: 65534

Many devs such as google believe that we should just avoid unsigned integers

This is because of two behaviors that can cause problems

First with signed values it takes a little work to accidentally overflow the top or bottom of the range because those values are far from 0. With unsigned numbers it is alot easier to overflow the bottom of the range, because the bottom of the range is 0 which is closer than the values are. Think about it this way since signed integers can hold negative values say you were storing the value 3 as an unsigned integer well all the "attacker" would have to do is find a way to subtract that variable by -4 and now the value of that variable would be 65535 or whatever the Length of the Unsigned integer is. With signed integers you would have to subtract WAYYYY more shit to get to that result. 



Consider the subtraction of two unsigned numbers, such as 2 and 3:

```cpp
#include <iostream>

// assume int is 4 bytes
int main()
{
	unsigned int x{ 2 };
	unsigned int y{ 3 };

	std::cout << x - y << '\n'; // prints 4294967295 (incorrect!)

	return 0;
}
```

Copy

You and I know that `2 - 3` is `-1`, but `-1` can’t be represented as an unsigned integer, so we get overflow and the following result:

4294967295



Another common unwanted wrap-around happens when an unsigned integer is repeatedly decremented by 1, until it tries to decrement to a negative number. You’ll see an example of this when loops are introduced.

Second, and more insidiously, unexpected behavior can result when you mix signed and unsigned integers. In C++, if a mathematical operation (e.g. arithmetic or comparison) has one signed integer and one unsigned integer, the signed integer will usually be converted to an unsigned integer. And the result will thus be unsigned. For example:

```cpp
#include <iostream>

// assume int is 4 bytes
int main()
{
	unsigned int u{ 2 };
	signed int s{ 3 };

	std::cout << u - s << '\n'; // 2 - 3 = 4294967295

	return 0;
}
```

Copy

In this case, if `u` was signed, the correct result would be produced. But because `u` is unsigned (which is easy to miss), `s` gets converted to unsigned, and the result (`-1`) is treated as an unsigned value. Since `-1` can’t be stored in an unsigned value, so we get overflow and an unexpected answer.


Here’s another example:

```cpp
#include <iostream>

// assume int is 4 bytes
int main()
{
    signed int s { -1 };
    unsigned int u { 1 };

    if (s < u) // -1 is implicitly converted to 4294967295, and 4294967295 < 1 is false
        std::cout << "-1 is less than 1\n";
    else
        std::cout << "1 is less than -1\n"; // this statement executes

    return 0;
}
```

Copy

This program is well formed, compiles, and is logically consistent to the eye. But it prints the wrong answer. And while your compiler should warn you about a signed/unsigned mismatch in this case, your compiler will also generate identical warnings for other cases that do not suffer from this problem (e.g. when both numbers are positive), making it hard to detect when there is an actual problem.


The author of doSomething() was expecting someone to call this function with only positive numbers. But the caller is passing in _-1_ -- clearly a mistake, but one made regardless. What happens in this case?

The signed argument of `-1` gets implicitly converted to an unsigned parameter. `-1` isn’t in the range of an unsigned number, so it wraps around to 4294967295. Then your program goes ballistic.



Best practice

Favor signed numbers over unsigned numbers for holding quantities (even quantities that should be non-negative) and mathematical operations. Avoid mixing signed and unsigned numbers.


First, unsigned numbers are preferred when dealing with bit manipulation (covered in chapter O -- that’s a capital ‘o’, not a ‘0’). They are also useful when well-defined wrap-around behavior is required (useful in some algorithms like encryption and random number generation).

Second, use of unsigned numbers is still unavoidable in some cases, mainly those having to do with array indexing. We’ll talk more about this in the lessons on arrays and array indexing.

Also note that if you’re developing for an embedded system (e.g. an Arduino) or some other processor/memory limited context, use of unsigned numbers is more common and accepted (and in some cases, unavoidable) for performance reasons.