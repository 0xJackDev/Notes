
Most programs that have a user interface of some kind need to handle user input. In the programs that you have been writing, you have been using std::cin to ask the user to enter text input. Because text input is so free-form (the user can enter anything), it’s very easy for the user to enter input that is not expected.

As you write programs, you should always consider how users will (unintentionally or otherwise) misuse your programs. A well-written program will anticipate how users will misuse it, and either handle those cases gracefully or prevent them from happening in the first place (if possible). A program that handles error cases well is said to be **robust**.

In this lesson, we’ll take a look specifically at ways the user can enter invalid text input via std::cin, and show you some different ways to handle those cases.



Before we discuss how `std::cin` and `operator>>` can fail, let’s recap how they work.



Here’s a simplified view of how `operator>>` works for input:

1. First, leading whitespace (spaces, tabs, and newlines at the front of the buffer) is discarded from the input buffer. This will discard any unextracted newline character remaining from a prior line of input.
2. If the input buffer is now empty, `operator>>` will wait for the user to enter more data. Leading whitespace is again discarded.
3. `operator>>` then extracts as many consecutive characters as it can, until it encounters either a newline character (representing the end of the line of input) or a character that is not valid for the variable being extracted to.

The result of the extraction is as follows:

- If any characters were extracted in step 3 above, extraction is a success. The extracted characters are converted into a value that is then assigned to the variable.
- If no characters could be extracted in step 3 above, extraction has failed. The object being extracted to is assigned the value `0` (as of C++11), and any future extractions will immediately fail (until `std::cin` is cleared).




The result of the extraction is as follows:

- If any characters were extracted in step 3 above, extraction is a success. The extracted characters are converted into a value that is then assigned to the variable.
- If no characters could be extracted in step 3 above, extraction has failed. The object being extracted to is assigned the value `0` (as of C++11), and any future extractions will immediately fail (until `std::cin` is cleared).


Validating input

The process of checking whether user input conforms to what the program is expecting is called **input validation**.

There are three basic ways to do input validation:

Inline (as the user types):

1. Prevent the user from typing invalid input in the first place.

Post-entry (after the user types):

2. Let the user enter whatever they want into a string, then validate whether the string is correct, and if so, convert the string to the final variable format.
3. Let the user enter whatever they want, let std::cin and operator>> try to extract it, and handle the error cases.



Types of invalid text input

We can generally separate input text errors into four types:

- Input extraction succeeds but the input is meaningless to the program (e.g. entering ‘k’ as your mathematical operator).
- Input extraction succeeds but the user enters additional input (e.g. entering ‘*q hello’ as your mathematical operator).
- Input extraction fails (e.g. trying to enter ‘q’ into a numeric input).
- Input extraction succeeds but the user overflows a numeric value.

Thus, to make our programs robust, whenever we ask the user for input, we ideally should determine whether each of the above can possibly occur, and if so, write code to handle those cases.

Let’s dig into each of these cases, and how to handle them using std::cin.



Error case 1: Extraction succeeds but input is meaningless

This is the simplest case. Consider the following execution of the above program:

Enter a decimal number: 5
Enter one of the following: +, -, *, or /: k
Enter a decimal number: 7

In this case, we asked the user to enter one of four symbols, but they entered ‘k’ instead. ‘k’ is a valid character, so std::cin happily extracts it to variable op, and this gets returned to main. But our program wasn’t expecting this to happen, so it doesn’t properly deal with this case (and thus never outputs anything).

The solution here is simple: do input validation. This usually consists of 3 steps:

1. Check whether the user’s input was what you were expecting.
2. If so, return the value to the caller.
3. If not, tell the user something went wrong and have them try again.

Here’s an updated getOperator() function that does input validation.

```cpp
char getOperator()
{
    while (true) // Loop until user enters a valid input
    {
        std::cout << "Enter one of the following: +, -, *, or /: ";
        char operation{};
        std::cin >> operation;

        // Check whether the user entered meaningful input
        switch (operation)
        {
        case '+':
        case '-':
        case '*':
        case '/':
            return operation; // return it to the caller
        default: // otherwise tell the user what went wrong
            std::cout << "Oops, that input is invalid.  Please try again.\n";
        }
    } // and try again
}
```

Copy

As you can see, we’re using a while loop to continuously loop until the user provides valid input. If they don’t, we ask them to try again until they either give us valid input, shutdown the program, or destroy their computer.






Error case 2: Extraction succeeds but with extraneous input

Consider the following execution of the above program:

Enter a decimal number: 5*7

What do you think happens next?

Enter a decimal number: 5*7
Enter one of the following: +, -, *, or /: Enter a decimal number: 5 * 7 is 35

The program prints the right answer, but the formatting is all messed up. Let’s take a closer look at why.

When the user enters `5*7` as input, that input goes into the buffer. Then operator>> extracts the 5 to variable x, leaving `*7\n` in the buffer. Next, the program prints “Enter one of the following: +, -, *, or /:”. However, when the extraction operator was called, it sees `*7\n` waiting in the buffer to be extracted, so it uses that instead of asking the user for more input. Consequently, it extracts the ‘*’ character, leaving `7\n` in the buffer.

After asking the user to enter another decimal number, the `7` in the buffer gets extracted without asking the user. Since the user never had an opportunity to enter additional data and hit enter (causing a newline), the output prompts all run together on the same line.

Although the above program works, the execution is messy. It would be better if any extraneous characters entered were simply ignored. Fortunately, it’s easy to ignore characters:

```cpp
std::cin.ignore(100, '\n');  // clear up to 100 characters out of the buffer, or until a '\n' character is removed
```

Copy

This call would remove up to 100 characters, but if the user entered more than 100 characters we’ll get messy output again. To ignore all characters up to the next ‘\n’, we can pass `std::numeric_limits<std::streamsize>::max()` to `std::cin.ignore()`. `std::numeric_limits<std::streamsize>::max()` returns the largest value that can be stored in a variable of type `std::streamsize`. Passing this value to `std::cin.ignore()` causes it to disable the count check.

To ignore everything up to and including the next ‘\n’ character, we call

```cpp
std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
```

Copy

Because this line is quite long for what it does, it’s handy to wrap it in a function which can be called in place of `std::cin.ignore()`.

```cpp
#include <limits> // for std::numeric_limits

	void ignoreLine()
	{
	    std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
	}
```

Copy

Since the last character the user entered is typically a ‘\n’, we can tell std::cin to ignore buffered characters until it finds a newline character (which is removed as well).

Let’s update our getDouble() function to ignore any extraneous input:

```cpp
double getDouble()
{
    std::cout << "Enter a decimal number: ";
    double x{};
    std::cin >> x;

    ignoreLine();
    return x;
}
```

Copy

Now our program will work as expected, even if we enter “5*7” for the first input -- the 5 will be extracted, and the rest of the characters will be removed from the input buffer. Since the input buffer is now empty, the user will be properly asked for input the next time an extraction operation is performed!s




Error case 3: Extraction fails

Extraction fails when no input can be extracted to the specified variable.

Now consider the following execution of our updated calculator program:

Enter a decimal number: a

You shouldn’t be surprised that the program doesn’t perform as expected, but how it fails is interesting:

Enter a decimal number: a
Enter one of the following: +, -, *, or /: Oops, that input is invalid.  Please try again.
Enter one of the following: +, -, *, or /: Oops, that input is invalid.  Please try again.
Enter one of the following: +, -, *, or /: Oops, that input is invalid.  Please try again.

and that last line keeps printing until the program is closed.

This looks pretty similar to the extraneous input case, but it’s a little different. Let’s take a closer look.

When the user enters ‘a’, that character is placed in the buffer. Then operator>> tries to extract ‘a’ to variable x, which is of type double. Since ‘a’ can’t be converted to a double, operator>> can’t do the extraction. Two things happen at this point: ‘a’ is left in the buffer, and std::cin goes into “failure mode”.

Once in “failure mode”, future requests for input extraction will silently fail. Thus in our calculator program, the output prompts still print, but any requests for further extraction are ignored. This means that instead waiting for us to enter an operation, the input prompt is skipped, and we get stuck in an infinite loop because there is no way to reach one of the valid cases.

In order to get `std::cin` working property again, we typically need do three things:

- Detect that a prior extraction has failed.
- Put `std::cin` back in normal operation mode.
- Remove the input that caused the failure (so the next extraction request doesn’t fail in an identical manner).

Here’s what that looks like:

```cpp
if (std::cin.fail()) // If the previous extraction failed
{
    // Let's handle the failure
    std::cin.clear(); // Put us back in 'normal' operation mode
    ignoreLine();     // And remove the bad input
}
```

Copy

Because `std::cin` has a Boolean conversion indicating whether the last input succeeded, it’s more idiomatic to write the above as following:

```cpp
if (!std::cin) // If the previous extraction failed
{
    // Let's handle the failure
    std::cin.clear(); // Put us back in 'normal' operation mode
    ignoreLine();     // And remove the bad input
}
```

Copy

Key insight

Once an extraction has failed, future requests for input extraction (including calls to `ignore()`) will silently fail until the `clear()` function is called. Thus, after detecting a failed extraction, calling `clear()` is usually the first thing you should do.

Let’s integrate that into our getDouble() function:

```cpp
double getDouble()
{
    while (true) // Loop until user enters a valid input
    {
        std::cout << "Enter a decimal number: ";
        double x{};
        std::cin >> x;

        if (!std::cin) // If the previous extraction failed
        {
            // Let's handle the failure
            std::cin.clear(); // Put us back in 'normal' operation mode
            ignoreLine();     // And remove the bad input
            continue;
        }

        // Our extraction succeeded
        ignoreLine(); // Ignore any additional input on this line
        return x;     // Return the value we extracted
    }
}
```

Copy

For fundamental types, a failed extraction due to invalid input will cause the variable to be assigned the value `0` (or whatever value `0` converts to in the variable’s type).

It is fine to call `clear()` even when extraction hasn’t failed -- it won’t do anything. In cases where we are going to call `ignoreLine()` regardless of whether we succeeded or failed, we can essentially combine the two cases:

```cpp
double getDouble()
{
    while (true) // Loop until user enters a valid input
    {
        std::cout << "Enter a decimal number: ";
        double x{};
        std::cin >> x;

        bool success { std::cin }; // Remember whether we had a successful extraction
        std::cin.clear();          // Put us back in 'normal' operation mode (in case we failed)
        ignoreLine();              // Ignore any additional input on this line (regardless)

        if (success)               // If we actually extracted a value
            return x;              // Return it (otherwise, we go back to top of loop)
    }
}
```

Copy

On Unix systems, entering an end-of-file (EOF) character (via ctrl-D) closes the input stream. This is something that `std::cin.clear()` can’t fix, so `std::cin` never leaves failure mode, which causes all subsequent input operations to fail. When this happens inside an infinite loop, your program will then loop endlessly until killed. To handle this case more elegantly, you can explicitly test for EOF using `std::cin.eof()`.

Because clearing a failed input stream is something we’re likely to be checking for a lot, this is a good candidate for a reusable function:

```cpp
// returns true if extraction failed, false otherwise
bool clearFailedExtraction()
{
    // Check for failed extraction
    if (!std::cin) // If the previous extraction failed
    {
        if (std::cin.eof()) // If the stream was closed
        {
            std::exit(0); // Shut down the program now
        }

        // Let's handle the failure
        std::cin.clear(); // Put us back in 'normal' operation mode
        ignoreLine();     // And remove the bad input

        return true;
    }

    return false;
}
```


Error case 4: Extraction succeeds but the user overflows a numeric value

Consider the following simple example:

```cpp
#include <cstdint>
#include <iostream>

int main()
{
    std::int16_t x{}; // x is 16 bits, holds from -32768 to 32767
    std::cout << "Enter a number between -32768 and 32767: ";
    std::cin >> x;

    std::int16_t y{}; // y is 16 bits, holds from -32768 to 32767
    std::cout << "Enter another number between -32768 and 32767: ";
    std::cin >> y;

    std::cout << "The sum is: " << x + y << '\n';
    return 0;
}
```

Copy

What happens if the user enters a number that is too large (e.g. 40000)?

Enter a number between -32768 and 32767: 40000
Enter another number between -32768 and 32767: The sum is: 32767

In the above case, `std::cin` goes immediately into “failure mode”, but also assigns the closest in-range value to the variable. When the entered value is larger than the largest possible value for the type, the closest in-range value is the largest possible value for the type. Consequently, `x` is left with the assigned value of `32767`. Additional inputs are skipped, leaving `y` with the initialized value of `0`. We can handle this kind of error in the same way as a failed extraction.




Putting it all together


Heres MY example that i coded to solve all these problems.
```
#include <iostream>
void ignoreLine()
{
	std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}



int math() {
	while (true) {
		int a{};
		int b{};
		char c{};
		std::cout << "Enter a number\n";
		std::cin >> a;
		if (!std::cin) {
			std::cin.clear();
			ignoreLine();
			continue;
		}
		ignoreLine();
		std::cout << "Enter a second number\n";
		std::cin >> b;
		if (!std::cin) {
			std::cin.clear();
			ignoreLine();
			continue;

		}
		ignoreLine();
		std::cout << "Enter a operator eg(+,-,*,/)\n";
		std::cin >> c;
		ignoreLine();

		switch (c) {
		case '+':
			return a + b;
		case '-':
			return a - b;
		case '*':
			return a * b;
		case '/':
			return a / b;
		default:
			std::cout << "Invalid Input try again.\n";

		}
	}
}

int main() {

	int result{ math() };
	std::cout << result;
}
```



and here is theirs
```
#include <cstdlib> // for std::exit
#include <iostream>
#include <limits> // for std::numeric_limits

void ignoreLine()
{
    std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}

// returns true if extraction failed, false otherwise
bool clearFailedExtraction()
{
    // Check for failed extraction
    if (!std::cin) // If the previous extraction failed
    {
        if (std::cin.eof()) // If the stream was closed
        {
            std::exit(0); // Shut down the program now
        }

        // Let's handle the failure
        std::cin.clear(); // Put us back in 'normal' operation mode
        ignoreLine();     // And remove the bad input

        return true;
    }

    return false;
}

double getDouble()
{
    while (true) // Loop until user enters a valid input
    {
        std::cout << "Enter a decimal number: ";
        double x{};
        std::cin >> x;

        if (clearFailedExtraction())
        {
            std::cout << "Oops, that input is invalid.  Please try again.\n";
            continue;
        }

        ignoreLine(); // Remove any extraneous input
        return x;     // Return the value we extracted
    }
}

char getOperator()
{
    while (true) // Loop until user enters a valid input
    {
        std::cout << "Enter one of the following: +, -, *, or /: ";
        char operation{};
        std::cin >> operation;

        if (!clearFailedExtraction()) // we'll handle error messaging if extraction failed below
             ignoreLine(); // remove any extraneous input (only if extraction succeded)

        // Check whether the user entered meaningful input
        switch (operation)
        {
        case '+':
        case '-':
        case '*':
        case '/':
            return operation; // Return the entered char to the caller
        default: // Otherwise tell the user what went wrong
            std::cout << "Oops, that input is invalid.  Please try again.\n";
        }
    }
}

void printResult(double x, char operation, double y)
{
    std::cout << x << ' ' << operation << ' ' << y << " is ";

    switch (operation)
    {
    case '+':
        std::cout << x + y << '\n';
        return;
    case '-':
        std::cout << x - y << '\n';
        return;
    case '*':
        std::cout << x * y << '\n';
        return;
    case '/':
        if (y == 0.0)
            break;

        std::cout << x / y << '\n';
        return;
    }

    std::cout << "???";  // Being robust means handling unexpected parameters as well, even though getOperator() guarantees operation is valid in this particular program
}

int main()
{
    double x{ getDouble() };
    char operation{ getOperator() };
    double y{ getDouble() };

    // Handle division by 0
    while (operation == '/' && y == 0.0)
    {
        std::cout << "The denominator cannot be zero.  Try again.\n";
        y = getDouble();
    }

    printResult(x, operation, y);

    return 0;
}
```

Conclusion

As you write your programs, consider how users will misuse your program, especially around text input. For each point of text input, consider:

- Could extraction fail?
- Could the user enter more input than expected?
- Could the user enter meaningless input?
- Could the user overflow an input?

You can use if statements and boolean logic to test whether input is expected and meaningful.

The following code will clear any extraneous input:

```cpp
#include <limits> // for std::numeric_limits

void ignoreLine()
{
    std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}
```

Copy

The following code will test for and fix failed extractions or overflow (and remove extraneous input):

```cpp
// returns true if extraction failed, false otherwise
bool clearFailedExtraction()
{
    // Check for failed extraction
    if (!std::cin) // If the previous extraction failed
    {
        if (std::cin.eof()) // If the stream was closed
        {
            std::exit(0); // Shut down the program now
        }

        // Let's handle the failure
        std::cin.clear(); // Put us back in 'normal' operation mode
        ignoreLine();     // And remove the bad input

        return true;
    }

    return false;
}
```

Copy

We can test to see if there is an unextracted input (other than a newline) as follows:

```cpp
// returns true if std::cin has unextracted input on the current line, false otherwise
bool hasUnextractedInput()
{
    return !std::cin.eof() && std::cin.peek() != '\n';
}
```

Copy

Finally, use loops to ask the user to re-enter input if the original input was invalid.



