


Modern debuggers contain one more debugging info window that can useful. This the call stack window


When your program calls a function you already know that it bookmarks the current location, makes the function call and then returns. How does it know where to return to? the answer is that it keeps track in the call stack. 



The **call stack** is a list of all the active functions that have been called to get to the current point of execution. The call stack includes an entry for each function called, as well as which line of code will be returned to when the function returns. Whenever a new function is called, that function is added to the top of the call stack. When the current function returns to the caller, it is removed from the top of the call stack, and control returns to the function just below it.

The **call stack window** is a debugger window that shows the current call stack. If you don’t see the call stack window, you will need to tell the IDE to show it.

For Visual Studio users

In Visual Studio, the call stack window can be found via _Debug menu > Windows > Call Stack_. Note that you have to be in a debug session to activate this window.


Your IDE may exhibit some differences:

- The format of your function names and line numbers may be different
- Your line numbers may be slightly different (off by 1)
- Instead of _[External Code]_ you may see a bunch of other crazily named functions.

These differences are inconsequential.

What’s relevant here is the top two lines. From the bottom up, we can see that function _main_ was called first, and then that function _a_ was called next.

The _line 5_ next to function _a_ shows us where the current point of execution is (which matches the execution marker in the code window). The _line 17_ on the second line indicates the line that will be returned to when control returns to function _main_.


The line numbers after the function names show the next line to be executed in each function.