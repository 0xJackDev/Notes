 More debugging tactics
In the previous lesson ([3.4 -- Basic debugging tactics](https://www.learncpp.com/cpp-tutorial/basic-debugging-tactics/)), we started exploring how to manually debug problems. In that lesson, we offered some criticisms of using statements to print debug text:

1. Debug statements clutter your code.
2. Debug statements clutter the output of your program.
3. Debug statements require modification of your code to both add and to remove, which can introduce new bugs.
4. Debug statements must be removed after you’re done with them, which makes them non-reusable.



Consider the following code


#include <iostream>

int getUserInput()
{
std::cerr << "getUserInput() called\n";
	std::cout << "Enter a number: ";
	int x{};
	std::cin >> x;
	return x;
}

int main()
{
std::cerr << "main() called\n";
    int x{ getUserInput() };
    std::cout << "You entered: " << x << '\n';

    return 0;
}



With these verbose errors you will either need to remove them or comment them out during your Production Environment. And if you want them later youll have to add them back or uncomment them.


One way to make it easier to disable debugging throughout your program is to make your debugging statements conditional Using preprocessor directories For example.

#include <iostream>

#define ENABLE_DEBUG // comment out to disable debugging

int getUserInput()
{
#ifdef ENABLE_DEBUG
std::cerr << "getUserInput() called\n";
#endif
	std::cout << "Enter a number: ";
	int x{};
	std::cin >> x;
	return x;
}

int main()
{
#ifdef ENABLE_DEBUG
std::cerr << "main() called\n";
#endif
    int x{ getUserInput() };
    std::cout << "You entered: " << x << '\n';

    return 0;
}


Then if you dont want the debugging you can just get rid of #define ENABLE_DEBUG and if you want it back you just add it back. *commenting* 





Using a logger.

An alternative approach to conditonalized debugging via the preprocessor is to send your debugging info to a log. A log is a sequential record of events that have happened, Usually time stamped. The process of generating a log is called logging. Typically logs are written to a file on disk (called a log file) so they can be reviewed later. Most applications and operating systems write log files that can be used to diagnose issues that occur.



Log files have a few advantages.
1. The Information in the log is separate to your programs output so you can avoid the clutter. 
2. Log files can be easily sent ot other people for diagnosis.



C++ contains an output stream named std::clog that is intended for writing logging information. However by default std::clog writes to the standard error stream (same as std::cerr) and while you can redirect to a file instead this is one area where you are generally better off using a third party toool. 




How you include, initialize, and use a logger will vary depending on the specific logger you select.



In larger or performance-sensitive projects, faster and more feature-rich loggers may be preferred, such as [spdlog](https://github.com/gabime/spdlog).

[

](https://www.learncpp.com/cpp-tutorial/using-an-integrated-debugger-stepping/)