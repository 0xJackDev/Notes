# Using an integrated debugger: Watching variables




In the previous lessons we learned how to use breakpoints and how to jump through our code. 



Watching a variable is the process of inspecting the value of a variable while the program is executing in debug mode.  There are several ways to do this.


The easiest way to examine the value of a simple variable like x is to hover your mouse over the variable x. Some modern debuggers support this method of inspecting simple variables, and it is the most straightforward way to do so. Make sure your hovering over the actual varaible and not just the line for example make sure if its int x{1}; make sure your cursor is over the x part.



If you’re using Visual Studio, you can also use QuickWatch. Highlight the variable name x with your mouse, and then choose “QuickWatch” from the right-click menu.



Setting a breakpoint on watched variables

Some debuggers will allow you to set a breakpoint on a watched variable rather than a line. This will cause the program to stop execution whenever the value of that variable changes.

For example, setting such a breakpoint on variable `x` in the above program will cause the debugger to stop after executing lines 8 and 11 (which is where the value of `x` is changed).

For Visual Studio users

In Visual Studio, make sure your variable is being watched. Next, _step into_ your program and go to the watch window. Right click on the variable and select “Break when value changes”.

You will need to re-enable “Break when value changes” each time you start a debugging session.


The watch window can evaluate expressions too

The watch window will also allow you to evaluate simple expressions. If you haven’t already, _run to cursor_ to line 12. Then try entering _x + 2_ into the watch window and see what happens (it should evaluate to 8).



Local watches

Because inspecting the value of local variables inside a function is common while debugging, many debuggers will offer some way to quickly watch the value of _all_ local variables in scope.

For Visual Studio users

In Visual Studio, you can see the value of all local variables in the _Locals_ window, which can be found at _Debug menu > Windows > Locals_. Note that you have to be in a debug session to activate this window.