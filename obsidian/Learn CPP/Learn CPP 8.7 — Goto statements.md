
The next kind of control flow statement we’ll cover is the unconditional jump. An unconditional jump causes execution to jump to another spot in the code. The term “unconditional” means the jump always happens (unlike an if-statement or switch-statement, where the jump only happens conditionally based on the result of an expression).

In C++, unconditional jumps are implemented via a **goto statement**, and the spot to jump to is identified through use of a **statement label**. Just like with switch case labels, statement labels are conventionally not indented.

The following is an example of a goto statement and statement label:

```cpp
#include <iostream>
#include <cmath> // for sqrt() function

int main()
{
    double x{};
tryAgain: // this is a statement label
    std::cout << "Enter a non-negative number: ";
    std::cin >> x;

    if (x < 0.0)
        goto tryAgain; // this is the goto statement

    std::cout << "The square root of " << x << " is " << std::sqrt(x) << '\n';
    return 0;
}
```

Copy

In this program, the user is asked to enter a non-negative number. However, if a negative number is entered, the program utilizes a goto statement to jump back to the `tryAgain` label. The user is then asked again to enter a new number. In this way, we can continually ask the user for input until he or she enters something valid.

Here’s a sample run of this program:

Enter a non-negative number: -4
Enter a non-negative number: 4
The square root of 4 is 2



Avoid using goto

Use of `goto` is shunned in C++ (and other modern high level languages as well). [Edsger W. Dijkstra](https://en.wikipedia.org/wiki/Edsger_Dijkstra), a noted computer scientist, laid out the case for avoiding goto in a famous but difficult to read paper called [Go To Statement Considered Harmful](http://www.cs.utexas.edu/users/EWD/ewd02xx/EWD215.PDF). The primary problem with goto is that it allows a programmer to jump around the code arbitrarily. This creates what is not-so-affectionately known as spaghetti code. **Spaghetti code** is code that has a path of execution that resembles a bowl of spaghetti (all tangled and twisted), making it extremely difficult to follow the logic of such code.

As Dijkstra says somewhat humorously, “the quality of programmers is a decreasing function of the density of go to statements in the programs they produce”.

Almost any code written using a goto statement can be more clearly written using other constructs in C++, such as if-statements and loops. One notable exception is when you need to exit a nested loop but not the entire function -- in such a case, a goto to just beyond the loops is probably the cleanest solution.


