
The debugger is a computer program that allows the programmer to control how another program executes and examine the program state while that program is running.  For example, the programmer can use a debugger to execute a program line by line, examining the value of variables along the way. By comparing the actual value of variables to what is expected, or watching the path of execution through the code, the debugger can help immensely in tracking down semantic (logic) errors.




Initially, debuggers (such as [gdb](https://en.wikipedia.org/wiki/Gdb)) were separate programs that had command-line interfaces, where the programmer had to type arcane commands to make them work.



step into 
The step into command executes the next statement in normal execution path of the program and then pauses the program so we can examine the programs state using a debugger. If the statement being executed contains a function call, step into causes the program to jump to the top of the function. 



Warning

Because operator<< is implemented as a function, your IDE may step into the implementation of operator<< instead.

If this happens, you’ll see your IDE open a new code file, and the arrow marker will move to the top of a function named operator<< (this is part of the standard library). Close the code file that just opened, then find and execute _step out_ debug command (instructions are below under the “step out” section, if you need help).




Step over

Like _step into_, The **step over** command executes the next statement in the normal execution path of the program. However, whereas _step into_ will enter function calls and execute them line by line, _step over_ will execute an entire function without stopping and return control to you after the function has been executed.



**Step out**

Unlike the other two stepping commands, **Step out** does not just execute the next line of code. Instead, it executes all remaining code in the function currently being executed, and then returns control to you when the function has returned.


A step too far

When stepping through a program, you can normally only step forward. It’s very easy to accidentally step past (overstep) the place you wanted to examine.

If you step past your intended destination, the usual thing to do is stop debugging and restart debugging again, being a little more careful not to pass your target this time.