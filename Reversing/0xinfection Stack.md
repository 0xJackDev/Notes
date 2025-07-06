
Part 15: Stack

In sum the stack is a special region of memory that stores temporary variables created by each function including main. The stack is a Last in first out data structure which is managed by the CPU closely. Every time a function declares a new variable it is pushed onto the stack. Every time a function exists all of the variables pushed onto the stack by that function are freed or deleted. Once a stack variable is freed that region of memory becomes available for other stack variables

The advantage of the stack to store variables is that memory is managed for you. You do not have to allocate memory manually or free it manually. The CPU manages and organizes stack memory very efficiently and is very fast.





Functions are the most fundamental feature in software development. A function allows you to organize code in a logical way to execute a specified task. It is not critical that you understand how functions work at this stage but it is important that you understand that when we develop. We want to minimize duplication using functions. DRY


When a program starts to execute a certain contiguous section of memory is set aside for the program called the stack. 


The stack pointer is a register that contains the top of the stack. The stack pointer contains the smallest address. lets say for example 0x00001000, such that any addresses smaller than 0x00001000 is considered garabage and any address greater than 0x00001000 is considered valid.

The above address is random and is not an absolute where you will find the stack pointer from program to program as it will vary. Lets look at what the stack looks like from an abstract perspective:

![](https://0xinfection.github.io/reversing/imgs/1520235829712.jpg)


The above diagram is what to keep clear in your mind as it is what is actually happening in memory. The next series of diagrams will show the opposite.


You will see the stack growing upward in the below diagrams however in reality it is growing downward from higher memory to lower memory.

In the addMe example below, the stack pointer (ESP), when examined in memory on a breakpoint on the main function, lists 0xffffd050. When the program calls the addMe function from main, ESP is now 0xffffd030 which is LOWER in memory. Therefore the stack grows DOWNWARD despite the diagram showing it pointing upward. Just keep in mind when the arrows below are pointing upward they are actually pointing to lower memory addresses.

The stack bottom is the largest valid address of the stack and is located in the larger address area or top of the memory model. This can be confusing as the stack bottom is higher in memory. The stack grows downward in memory and it is critical that you understand that now as we go forward.

The stack limit is the smallest valid address of the stack. If the stack pointer gets smaller than this, there is a stack overflow which can corrupt a program to allow an attacker to take control of a system. Malware attempts to take advantage of stack overflows. As of recent, there are protections build into modern OS that attempt to prevent this from happening.

There are two operations on the stack which are push and pop. You can push one or more registers by setting the stack pointer to a smaller value. This is usually done by subtracting four times the number of registers to be pushed onto the stack and copying the registers to the stack.

You can pop one or more registers by copying the data from the stack to the registers, then to add a value to the stack pointer. This is usually done by adding four times the number of registers to be popped on the stack.

Let us look at how the stack is used to implement functions. For each function call there is a section of the stack reserved for the function. This is called the stack frame.

Let’s look at the C program we created in tutorial 12 and examine what the main function looks like:

![](https://0xinfection.github.io/reversing/imgs/1520622740099.jpg)

We see two functions here. The first one is the unreachableFunction to which will never execute under normal circumstances and we also see the main function that will always be the first function to be called onto the stack.

When we run this program, the stack will look like this:

![](https://0xinfection.github.io/reversing/imgs/1520622738609.jpg)


We can see the stack frame for the int main(void) above. It is also referred to as the activation record. A stack frame exists whenever a function has started but is yet to complete. For example inside the body of the main function there is a call to the addMe function which takes two argurments. There needs to be assembly language code in 

There needs to be assembly language code in int main(void) to push the arguments for int addMe(int a, int b) onto the stack. Lets examine some code.

![](https://0xinfection.github.io/reversing/imgs/1520231875596.jpg)

When we compile and run this program we will see the value of 5 to be print out like this:

![](https://0xinfection.github.io/reversing/imgs/1520622737902.jpg)

Very simply, int main(void) calls int addMe(int a, int b) first and will get put on the stack like this:

![](https://0xinfection.github.io/reversing/imgs/1520144504701.jpg)

You can see that by placing the arguments on the stack, the stack frame for **int main(void)** has increased in size. We also reserved space for the return value which is computed by **int addMe(int a, int b)** and when the function returns, the return value in **int main(void)** gets restored and execution continues in **int main(void)** until it finishes.

Once we get the instructions for **int addMe(int a, int b)**, the function may need local variables so the function needs to push some space on the stack which would look like:

![](https://0xinfection.github.io/reversing/imgs/1520622739277.jpg)

**int addMe(int a, int b)** can access the arguments passed to it from **int main(void)** because the code in **int main(void)** places the arguments just as **int addMe(int a, int b)** expects it. 

FP is the frame pointer and points to the location where the stack pointer was just before **int addMe(int a, int b)** moved the stack pointer or SP for int **addMe(int a, int b)**’s own local variables.

The use of a frame pointer is essential when a function is likely to move the stack pointer several times throughout the course of running the function. The idea is to keep the frame pointer fixed for the duration of **int addMe(int a, int b)**’s stack frame. In the meantime, the stack pointer can change values.

We can use the frame pointer to compute the locations in memory for both arguments as well as local variables. Since it does not move, the computations for those locations should be some fixed offset from the frame pointer.

Once it is time to exit **int addMe(int a, int b)**, the stack pointer is set to where the frame pointer is which pops off the **int addMe(int a, int b)** stack frame.


