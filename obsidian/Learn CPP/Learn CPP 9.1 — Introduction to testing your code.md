
So, you’ve written a program, it compiles, and it even appears to work! What now?

Well, it depends. If you’ve written your program to be run once and discarded, then you’re done. In this case, it may not matter that your program doesn’t work for every case -- if it works for the one case you needed it for, and you’re only going to run it once, then you’re done.


If your program is entirely linear (has no conditionals, such as _if statements_ or _switch statements_), takes no inputs, and produces the correct answer, then you’re probably done. In this case, you’ve already tested the entire program by running it and validating the output. You may want to compile and run the program on several different systems to ensure it behaves consistently (if it doesn’t, you’ve probably done something that produces undefined behavior that just happens to work anyway on your initial system).



But most likely you’ve written a program you intend to run many times, that uses loops and conditional logic, and accepts user input of some kind. You’ve possibly written functions that may be reusable in other future programs. You may have experienced a bit of **scope creep**, where you added some new capabilities that were originally not planned for. Maybe you’re even intending to distribute this program to other people (who are likely to try things you haven’t thought of). In this case, you really should be validating that your program works like you think it does under a wide variety of conditions -- and that requires some proactive testing.




Best practice

Write your program in small, well defined units (functions or classes), compile often, and test your code as you go.




Informal testing

One way you can test code is to do informal testing as you write the program. After writing a unit of code (a function, a class, or some other discrete “package” of code), you can write some code to test the unit that was just added, and then erase the test once the test passes. As an example, for the following isLowerVowel() function, you might write the following code:

```cpp
#include <iostream>

// We want to test the following function
// For simplicity, we'll ignore that 'y' is sometimes counted as a vowel
bool isLowerVowel(char c)
{
    switch (c)
    {
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        return true;
    default:
        return false;
    }
}

int main()
{
    // So here's our temporary tests to validate it works
    std::cout << isLowerVowel('a') << '\n'; // temporary test code, should produce 1
    std::cout << isLowerVowel('q') << '\n'; // temporary test code, should produce 0

    return 0;
}
```

Copy

If the results come back as `1` and `0`, then you’re good to go. You know your function works for some basic cases, and you can reasonably infer by looking at the code that it will work for the cases you didn’t test (‘e’, ‘i’, ‘o’, and ‘u’). So you can erase that temporary test code, and continue programming.




Preserving your tests

Although writing temporary tests is a quick and easy way to test some code, it doesn’t account for the fact that at some point, you may want to test that same code again later. Perhaps you modified a function to add a new capability, and want to make sure you didn’t break anything that was already working. For that reason, it can make more sense to preserve your tests so they can be run again in the future. For example, instead of erasing your temporary test code, you could move the tests into a testVowel() function:

```cpp
#include <iostream>

bool isLowerVowel(char c)
{
    switch (c)
    {
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        return true;
    default:
        return false;
    }
}

// Not called from anywhere right now
// But here if you want to retest things later
void testVowel()
{
    std::cout << isLowerVowel('a') << '\n'; // temporary test code, should produce 1
    std::cout << isLowerVowel('q') << '\n'; // temporary test code, should produce 0
}

int main()
{
    return 0;
}
```

Copy

As you create more tests, you can simply add them to the `testVowel()` function.




Automating your test functions

One problem with the above test function is that it relies on you to manually verify the results when you run it. This requires you to remember what the expected answer was at worst (assuming you didn’t document it), and manually compare the actual results to the expected results.

We can do better by writing a test function that contains both the tests AND the expected answers and compares them so we don’t have to.

```cpp
#include <iostream>

bool isLowerVowel(char c)
{
    switch (c)
    {
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        return true;
    default:
        return false;
    }
}

// returns the number of the test that failed, or 0 if all tests passed
int testVowel()
{
    if (!isLowerVowel('a')) return 1;
    if (isLowerVowel('q')) return 2;

    return 0;
}

int main()
{
    int result { testVowel() };
    if (result != 0)
        std::cout << "testVowel() test " << result << " failed.\n";
    else
        std::cout << "testVowel() tests passed.\n";

    return 0;
}
```

Copy

Now, you can call `testVowel()` at any time to re-prove that you haven’t broken anything, and the test routine will do all the work for you, returning either an “all good” signal (return value `0`), or the test number that didn’t pass, so you can investigate why it broke. This is particularly useful when going back and modifying old code, to ensure you haven’t accidentally broken anything!





Unit testing frameworks

Because writing functions to exercise other functions is so common and useful, there are entire frameworks (called **unit testing frameworks**) that are designed to help simplify the process of writing, maintaining, and executing unit tests. Since these involve third party software, we won’t cover them here, but you should be aware they exist.

Integration testing

Once each of your units has been tested in isolation, they can be integrated into your program and retested to make sure they were integrated properly. This is called an **integration test**. Integration testing tends to be more complicated -- for now, running your program a few times and spot checking the behavior of the integrated unit will suffice.


