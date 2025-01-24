

use the debugger and set breakpoints




How to Bypass Checking if a debugger is present.. Since ALl the detections are Just based on teh PEB.BeingDebugged Flag you can bypass them all with overwriting the beingDebugging flag with 0 or hook each function indivudually and change the return value to a spoof result.


POC for setting Debug Flag False

https://bitbucket.org/GH-Rake/patternscan/src/b65701b4ce7244e38eb0d2e2c5e8563132dada7a/debug.cpp?at=master&fileviewer=file-view-default


NtQueryInformationProcess with ProcessDebugPort argument retrieves a DWORD_PTR value that is the port number of the debugger for the process. A nonzero value indicates the process is being run under a ring 3 debugger.

Bypass:
Hook NtQueryInformatinProcess in the game process 

POC 

https://bitbucket.org/GH-Rake/patternscan/src/b65701b4ce7244e38eb0d2e2c5e8563132dada7a/debug.cpp?at=master&fileviewer=file-view-default

https://guidedhacking.com/threads/anti-debugging-tricks-hidden-threads.14281/




Make sure you step through code and Try to narrow down where the issue is with breakpoints


The Autos window in Visual Studio displays variables that are being acted on by the current function. This is useful for checking the state of your variables as you step through code



When working with an internal project you can attach the debugger to the process by clicking Debug then attach to process. In visual Studio. Now this will auto do it. 

