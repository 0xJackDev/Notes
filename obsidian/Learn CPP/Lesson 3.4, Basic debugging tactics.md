

Basic debugging tactics 



Commenting out your code. 


This is an easy one, if your program is exhibiting weird behavior one way to reduce the amount of code to search through is to comment some code out and see if the issue persists. If the issues remains the code you commented out probably wasn't responsible.


- If the problem goes away, then _doMaintenance_ must be causing the problem, and we should focus our attention there.

- If the problem is unchanged (which is more likely), then we can reasonably assume that _doMaintenance_ wasn’t at fault, and we can exclude the entire function from our search for now. This doesn’t help us understand whether the actual problem is before or after the call to _doMaintenance_, but it reduces the amount of code we have to subsequently look through.

- If commenting out _doMaintenance_ causes the problem to morph into some other related problem (e.g. the program stops printing names), then it’s likely that _doMaintenance_ is doing something useful that some other code is dependent on. In this case, we probably can’t tell whether the issue is in _doMaintenance_ or elsewhere, so we can uncomment _doMaintenance_ and try some other approach.





Debugging tactic 2: Validating your code flow.


Another common problem in complex programs is that a program is calling a function too many or too few times. 


In such cases it can be helpful to place statements at the top of your functions to print the functions name. That way when the program runs you can see what functions get called


When printing information  for debugging purposed use std::cerr instead of std::cout. This is because std::cout may be buffered meaning there is a pause between when you ask cout to output the information and when it actually does. If you output using cout and your code crashes immediately aftaward cout may have not output anything yet. So use std::cerr for errors.






Debugging tactic #3: printing values.


With some bugs the program may be calculating or passing the wrong value.

While adding debug statements to programs for diagnostic purposes is a common rudimentary technique, and a functional one (especially when a debugger is not available for some reason), it’s not that great for a number of reasons:

1. Debug statements clutter your code.
2. Debug statements clutter the output of your program.
3. Debug statements require modification of your code to both add and to remove, which can introduce new bugs.
4. Debug statements must be removed after you’re done with them, which makes them non-reusable.

