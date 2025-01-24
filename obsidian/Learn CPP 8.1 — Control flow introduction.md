

When a program is run, the CPU begins execution at the top of `main()`, executes some number of statements (in sequential order by default), and then the program terminates at the end of `main()`. The specific sequence of statements that the CPU executes is called the program’s **execution path** (or **path**, for short).



Categories of flow control statements

|Category|Meaning|Implemented in C++ by|
|---|---|---|
|Conditional statements|Causes a sequence of code to execute only if some condition is met.|if, else, switch|
|Jumps|Tells the CPU to start executing the statements at some other location.|goto, break, continue|
|Function calls|Jump to some other location and back.|function calls, return|
|Loops|Repeatedly execute some sequence of code zero or more times, until some condition is met.|while, do-while, for, ranged-for|
|Halts|Terminate the program.|std::exit(), std::abort()|
|Exceptions|A special kind of flow control structure designed for error handling.|try, throw, catch|

We’ll cover all of these categories in detail throughout this chapter, with the exception of exceptions (ha) which we’ll devote an entire future chapter to ([chapter 27](https://www.learncpp.com/#Chapter27)).