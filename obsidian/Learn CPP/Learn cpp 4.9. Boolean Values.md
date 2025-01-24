

Booleans are True and false.




To initialize or assign a `true` or `false` value to a Boolean variable, we use the keywords `true` and `false`.

```cpp
bool b1 { true };
bool b2 { false };
b1 = false;
bool b3 {}; // default initialize to false
```

Copy

Just as the unary minus operator (-) can be used to make an integer negative, the logical NOT operator (!) can be used to flip a Boolean value from `true` to `false`, or `false` to `true`:

```cpp
bool b1 { !true }; // b1 will be initialized with the value false
bool b2 { !false }; // b2 will be initialized with the value true
```

Boolean values are not actually stored in Boolean variables as the words “true” or “false”. Instead, they are stored as integral values: `true` is stored as integer `1`, and `false` is stored as integer `0`. Similarly, when Boolean values are evaluated, they don’t actually evaluate to “true” or “false”. They evaluate to the integers `0` (false) or `1` (true). Because Booleans store integral values, they are considered to be an integral type.




Printing Boolean values

When we print Boolean values, `std::cout` prints `0` for `false`, and `1` for `true`:

```cpp
#include <iostream>

int main()
{
    std::cout << true << '\n'; // true evaluates to 1
    std::cout << !true << '\n'; // !true evaluates to 0

    bool b {false};
    std::cout << b << '\n'; // b is false, which evaluates to 0
    std::cout << !b << '\n'; // !b is true, which evaluates to 1
    return 0;
}
```

Copy

Outputs:

1
0
0
1

If you want `std::cout` to print `true` or `false` instead of `0` or `1`, you can output `std::boolalpha`. This doesn’t output anything, but manipulates the way `std::cout` outputs bool values.

Here’s an example:

```cpp
#include <iostream>

int main()
{
    std::cout << true << '\n';
    std::cout << false << '\n';

    std::cout << std::boolalpha; // print bools as true or false

    std::cout << true << '\n';
    std::cout << false << '\n';
    return 0;
}
```

Copy

This prints:

1
0
true
false


You can use `std::noboolalpha` to turn it back off.


Integer to Boolean conversion

When using uniform initialization, you can initialize a variable using integer literals `0` (for `false`) and `1` (for `true`) (but you really should be using `false` and `true` instead). Other integer literals cause compilation errors:

```cpp
#include <iostream>

int main()
{
	bool bFalse { 0 }; // okay: initialized to false
	bool bTrue  { 1 }; // okay: initialized to true
	bool bNo    { 2 }; // error: narrowing conversions disallowed

	std::cout << bFalse << bTrue << bNo << '\n';

	return 0;
}
```




However, in any context where an integer can be converted to a Boolean, the integer `0` is converted to `false`, and any other integer is converted to `true`.


```cpp
#include <iostream>

int main()
{
	std::cout << std::boolalpha; // print bools as true or false

	bool b1 = 4 ; // copy initialization allows implicit conversion from int to bool
	std::cout << b1 << '\n';

	bool b2 = 0 ; // copy initialization allows implicit conversion from int to bool
	std::cout << b2 << '\n';


	return 0;
}
```

Copy

This prints:

true
false

Note: `bool b1 = 4;` may generate a warning. If so you’ll have to disable treating warnings as errors to compile the example.


Inputting Boolean values

Inputting Boolean values using `std::cin` sometimes trips new programmers up.

Consider the following program:

```cpp
#include <iostream>

int main()
{
	bool b{}; // default initialize to false
	std::cout << "Enter a boolean value: ";
	std::cin >> b;
	std::cout << "You entered: " << b << '\n';

	return 0;
}
```

Copy

Enter a Boolean value: true
You entered: 0

Wait, what?

It turns out that `std::cin` only accepts two inputs for Boolean variables: `0` and `1` (_not_ `true` or `false`). Any other inputs will cause `std::cin` to silently fail. In this case, because we entered `true`, `std::cin` silently failed. A failed input will also zero-out the variable, so `b` is assigned the value `false`. Consequently, when `std::cout` prints a value for `b`, it prints `0`.

To allow `std::cin` to accept `false` and `true` as inputs, you must first input to `std::boolalpha`:


```
int main()
{
	bool b{};

	std::cin >> std::boolalpha;
	std::cout << "please enter a true or false" << '\n';
	std::cin >> b; 

	std::cout << std::boolalpha;
	std::cout << "Your Boolean value is:" << b; 
	return 0;
}
```

As you see you must configure both std::cin and std::cout in order to incorporate inputting a Boolean value 

now lets make a if statement to interact with these
```

int main()
{
	bool b{};

	std::cin >> std::boolalpha;
	std::cout << "please enter a true or false" << '\n';
	std::cin >> b; 
	std::cout << std::boolalpha;


	if (b == true) {
		std::cout << 't';
	}
	else {
		std::cout << 'f';
	}
	return 0;
}
```

But there is a problem with this code. unless i type true in all lowercase it will print f. Say i input TRUE, this is because it directly assigns the variable and it isnt checking what string is being inputted so if im not using the correct syntax to assign a variable to true it will just say its false! 0 and 1 will also not be accepted since you enabled std::boolalpha;



Boolean return values

Boolean values are often used as the return values for functions that check whether something is true or not. Such functions are typically named starting with the word _is_ (e.g. isEqual) or _has_ (e.g. hasCommonDivisor).

Consider the following example, which is quite similar to the above:

```cpp
#include <iostream>

// returns true if x and y are equal, false otherwise
bool isEqual(int x, int y)
{
    return x == y; // operator== returns true if x equals y, and false otherwise
}

int main()
{
    std::cout << "Enter an integer: ";
    int x{};
    std::cin >> x;

    std::cout << "Enter another integer: ";
    int y{};
    std::cin >> y;

    std::cout << std::boolalpha; // print bools as true or false

    std::cout << x << " and " << y << " are equal? ";
    std::cout << isEqual(x, y) << '\n'; // will return true or false

    return 0;
}
```

Copy

Here’s output from two runs of this program:

Enter an integer: 5
Enter another integer: 5
5 and 5 are equal? true

Enter an integer: 6
Enter another integer: 4
6 and 4 are equal? false


How does this work? First we read in integer values for `x` and `y`. Next, the expression `isEqual(x, y)` is evaluated. In the first run, this results in a function call to `isEqual(5, 5)`. Inside that function, `5 == 5` is evaluated, producing the value `true`. The value `true` is returned back to the caller to be printed by `std::cout`. In the second run, the call to `isEqual(6, 4)` returns the value `false`.

Boolean values take a little bit of getting used to, but once you get your mind wrapped around them, they’re quite refreshing in their simplicity! Boolean values are also a huge part of the language -- you’ll end up using them more than all the other fundamental types put together!

We’ll continue our exploration of Boolean values in the next lesson.



