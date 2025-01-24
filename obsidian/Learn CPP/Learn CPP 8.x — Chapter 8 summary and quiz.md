
Chapter Review

The specific sequence of statements that the CPU executes in a program is called the program’s **execution path**. A **straight-line program** takes the same path every time it is run.

**Control flow statements** (also called **Flow control statements**) allow the programmer to change the normal path of execution. When a control flow statement causes the program to begin executing some non-sequential instruction sequence, this is called a **branch**.

A **conditional statement** is a statement that specifies whether some associated statement(s) should be executed or not.

**If statements** allow us to execute an associated statement based on whether some condition is `true`. **Else statements** execute if the associated condition is `false`. You can chain together multiple if and else statements.

A **dangling else** occurs when it is ambiguous which `if statement` an `else statement` is connected to. `Dangling else` statements are matched up with the last unmatched `if statement` in the same block. Thus, we trivially avoid `dangling else` statements by ensuring the body of an `if statement` is placed in a block.

A **null statement** is a statement that consists of just a semicolon. It does nothing, and is used when the language requires a statement to exist but the programmer does not need the statement to do anything.

**Switch statements** provide a cleaner and faster method for selecting between a number of matching items. Switch statements only work with integral types. **Case labels** are used to identify the values for the evaluated condition to match. The statements beneath a **default label** are executed if no matching case label can be found.

When execution flows from a statement underneath a label into statements underneath a subsequent label, this is called **fallthrough**. A `break statement` (or `return statement`) can be used to prevent fallthrough. The [[fallthrough]] attribute can be used to document intentional fallthrough.

**Goto statements** allow the program to jump to somewhere else in the code, either forward or backwards. These should generally be avoided, as they can create **spaghetti code**, which occurs when a program has a path of execution that resembles a bowl of spaghetti.

**While loops** allow the program to loop as long as a given condition evaluates to `true`. The condition is evaluated before the loop executes.

An **infinite loop** is a loop that has a condition that always evaluates to `true`. These loops will loop forever unless another control flow statement is used to stop them.

A **loop variable** (also called a **counter**) is an integer variable used to count how many times a loop has executed. Each execution of a loop is called an **iteration**.

**Do while loops** are similar to while loops, but the condition is evaluated after the loop executes instead of before.

**For loops** are the most used loop, and are ideal when you need to loop a specific number of times. An **off-by-one error** occurs when the loop iterates one too many or one too few times.

**Break statements** allow us to break out of a switch, while, do while, or for loop (also `range-based for loops`, which we haven’t covered yet). **Continue statements** allow us to move immediately to the next loop iteration.

**Halts** allow us to terminate our program. **Normal termination** means the program has exited in an expected way (and the `status code` will indicate whether it succeeded or not). **std::exit()** is automatically called at the end of `main`, or it can be called explicitly to terminate the program. It does some cleanup, but does not cleanup any local variables, or unwind the call stack.

**Abnormal termination** occurs when the program encountered some kind of unexpected error and had to be shut down. **std::abort** can be called for an abnormal termination.

An **algorithm** is a finite sequence of instructions that can be followed to solve some problem or produce some useful result. An algorithm is considered to be **stateful** if it retains some information across calls. Conversely, a **stateless** algorithm does not store any information (and must be given all the information it needs to work with when it is called). When applied to algorithms, the term **state** refers to the current values held in stateful variables.

An algorithm is considered **deterministic** if for a given input (the value provided for `start`) it will always produce the same output sequence.

A **pseudo-random number generator (PRNG)** is an algorithm that generates a sequence of numbers whose properties simulate a sequence of random numbers. When a PRNG is instantiated, an initial value (or set of values) called a **random seed** (or **seed** for short) can be provided to initialize the state of the PRNG. When a PRNG has been initialized with a seed, we say it has been **seeded**. The size of the seed value can be smaller than the size of the state of the PRNG. When this happens, we say the PRNG has been **underseeded**. The length of the sequence before a PRNG begins to repeat itself is known as the **period**.

A **random number distribution** converts the output of a PRNG into some other distribution of numbers. A **uniform distribution** is a random number distribution that produces outputs between two numbers X and Y (inclusive) with equal probability.



