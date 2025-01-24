Run to cursor

The first useful command is commonly called _Run to cursor_. This **Run to cursor** command executes the program until execution reaches the statement selected by your cursor. Then it returns control to you so you can debug starting at that point. This makes for an efficient way to start debugging at a particular point in your code, or if already debugging, to move straight to some place you want to examine further.


Continue

Once you’re in the middle of a debugging session, you may want to just run the program from that point forward. The easiest way to do this is to use the _continue_ command. The **continue** debug command simply continues running the program as per normal, either until the program terminates, or until something triggers control to return back to you again (such as a breakpoint, which we’ll cover later in this lesson).

For Visual Studio users

In Visual Studio, the _continue_ command can be accessed while already debugging a program via _Debug menu > Continue_, or by pressing the F5 shortcut key.



Start

The _continue_ command has a twin brother named _start_. The _start_ command performs the same action as _continue_, just starting from the beginning of the program. It can only be invoked when not already in a debug session.

For Visual Studio users

In Visual Studio, the _start_ command can be accessed while not debugging a program via _Debug menu > Start Debugging_, or by pressing the F5 shortcut key.





Breakpoints

The last topic we are going to talk about in this section is breakpoints. A **breakpoint** is a special marker that tells the debugger to stop execution of the program at the breakpoint when running in debug mode.

For Visual Studio users

In Visual Studio, you can set or remove a breakpoint via _Debug menu > Toggle Breakpoint_, or by right clicking on a statement and choosing _Toggle Breakpoint_ from the context menu, or by pressing the F9 shortcut key, or by clicking to the left of the line number (in the light grey area).


Breakpoints have a couple of advantages over _run to cursor_. First, a breakpoint will cause the debugger to return control to you every time they are encountered (unlike _run to cursor_, which only runs to the cursor once each time it is invoked). Second, you can set a breakpoint and it will persist until you remove it, whereas with _run to cursor_ you have to locate the spot you want to run to each time you invoke the command.

Note that breakpoints placed on lines that are not in the path of execution will not cause the debugger to halt execution of the code.



There’s one more debugging command that’s used fairly uncommonly, but is still at least worth knowing about, even if you won’t use it very often. The **set next statement** command allows us to change the point of execution to some other statement (sometimes informally called _jumping_). This can be used to jump the point of execution forwards and skip some code that would otherwise execute, or backwards and have something that already executed run again.

For Visual Studio users

In Visual Studio, you can jump the point of execution by right clicking on a statement and choosing _Set next statement_ from the context menu, or by pressing the Ctrl-Shift-F10 shortcut combination. This option is contextual and only occurs while already debugging a program.


In our exploration of basic debugging techniques, we discussed commenting out a function as a way to determine whether that function had a role in causing an issue. This requires modifying our code, and remembering to uncomment the function later. In the debugger, there’s no direct way to skip a function, so if you decide you want to do this, using _set next statement_ to jump over a function call is the easiest way to do so.