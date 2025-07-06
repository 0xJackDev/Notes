
Part 11:


The segment registers are used for referencing memory locations. there are three different methods of accessing system memory of which we will focus on the flat memory model.

There are six segment registers as follows:

CS: Code segment register stores the base location of the code section (.text section) which is used for data acess


DS: Data segment register stores the default location for variables (.data section) which is used for data access

ES: Extra segment register which is used during string operations.

SS: Stack segment register stores the base location of the stack segment and is used when implicit using the stack pointer or using the base pointer

FS: Extra Segment register

GS: Extra segment register


Each segment register is 16-bit and contains the pointer to the start of the memory-specific segment. The CS register contains the pointer to the code segment in memory. The code segment is where the instruction codes are stored in memory. The processor retrieves instruction codes from memory based on the CS register value and an offset value contained in the instruction ptr (EIP) register. Keep in mind no program can load or change the CS register. The processor assigns its values as the program is assigned memory space


THE DS. ES. FS, and GS segment registers are all used to put to data segments. Each of the four data segments help the program separate data elements to make sure they dont overlap. The program loads teh data segment registers with the appropriate pointer value for the segments and then reference individual memory locations using an offset.

The stack segment register (SS) is used to point to the stack segment. The stack contains data values passed to functions and procedures within the program

Segment registers are considered part of the OS and cant be changed directly. When working with the Protected mode flat model (x86 architecture which is 32-bit) your program runs and receives 4GB address space to which any 32-bit register can only express 4,294,967,296 different locations. If you have more than 4GB of memory in your computer, the OS must arrange a 4GB region within memory and your programs are limited to that new region. This task is completed by the segment registers and the OS keeps close control of this.




Part 12: Instruction pointer register

The instruction pointer register called the EIP register is simply the most import register you will deal with in reverse engineering. The EIP or instruction pointer keeps track of the next instruction to execute. EIP points to the next instruction to execute if you were to alter that pointer to jump to another area in the code you would have complete control.



Lets jump ahead and dive into some code.

mytechnotalent.com


![](https://0xinfection.github.io/reversing/imgs/1520572373327.jpg)

We have simply compiled the code to work with the IA32 instruction set and ran it. As you can see there is no call to the **unreachableFunction** of any kind as it is unreachable under normal conditions as you can see the ‘Hello World!` printed when executed.

![](https://0xinfection.github.io/reversing/imgs/1520572374855.jpg)

We have disassembled the program using the GDB Debugger. We have set a breakpoint on the main function and ran the program. The => shows where EIP is pointing to when we step to the next instruction. If we follow normal program flow, ‘Hello World! will print to the console and exit.

![](https://0xinfection.github.io/reversing/imgs/1520191047777.jpg)

If we run the program again and do an examination of where EIP is pointing to we will see:

![](https://0xinfection.github.io/reversing/imgs/1520173635003.jpg)

We can see EIP is pointing to main+17 or the address of 0x680cec83.

Lets examine the **unreachableFunction** and see where it starts in memory and write down that address.

![](https://0xinfection.github.io/reversing/imgs/1520572373912.jpg)

The next step is to set EIP to address 0x0804843b so that we hijack program flow to run the unreachableFunction.

![](https://0xinfection.github.io/reversing/imgs/1520572373288.jpg)

Now that we have hacked control of EIP, lets continue and watch how we have hijacked the operation of a running program to our advantage!

![](https://0xinfection.github.io/reversing/imgs/1520192688705.jpg)

Tada! We have hacked the program!




Part 13: Control Registers


There are five control registers used to determine the operating mode of the CPU and the characteristics of the current executing tasks

**CR0**: System flag that control the operating mode and various states of the processor.

**CR1**: (Not Currently Implemented)

**CR2**: Memory page fault information.

**CR3**: Memory page directory information.

**CR4**: Flags that enable processor feathers and indicate feature capabilities of the processor.


The values in each of the control registers can’t be directly accessed however the data in the control register can be moved to one of the general-purpose registers and once the data is in a GP register, a program can examine the bit flags in the register to determine the operating status of the processor in conjunction with the current running task.

If a change is required to a control register flag value, the change can be made to the data in the GP register and the register moved to the CR. Low-level System Programmers usually modify the values in control registers. Normal application programs do not usually modify control register entries however they might query flag values to determine the capabilities of the host processor chip on which the program is currently running.




part 14: Flags


The topic of flags is very complex. and complicated concepts of assembly and program flow control when reverse engineering is needed.


What is important is that flags help control, check and very program execution and are a mechanism to determine whether an operation performed by the CPU is successful or not.

Flags are critical to the ASM language applications as they are a check to verify each programs function successfully 

We are dealing with 32-bit ASM to which a single 32-bit register which contains a group of status, control and system flags exist. This register is called EFLAGS register as it contains 32 bits of information that are mapped to represent specific flags of info

There are three kinds of flags which are status flags, control flags and system flags.

Status flags are as follows:

**CF**: Carry Flag

**PF**: Parity Flag

**AF**: Adjust Flag

**ZF**: Zero Flag

**SF**: Sign Flag

**OF**: Overflow Flag

The carry flag is set when a math operation on a unsigned integer value generates a carry or borrow for the most significant bit. This is an overflow condition for the register involved in the math operation. When this occurs the remaining data in the register is not the correct answer the math operation

The parity flag is used to indicate corrupt data as a result of a math operation in a register. When checked, the parity flag is set if the total number of 1 bits in the result is even and is cleared if the total number of 1 bits in the result is odd. When the parity flag is checked, an application can determine whether the register has been corrupted since the operation.

The adjust flag is used in Binary Coded Decimal math operations and is set if a carry or borrow operation occurs from bit 3 of the register used for the calculation.

The zero flag is set if the result of an operation is zero.

The sign flag is set to the most significant bit of the result which is the sign bit and indicates whether the result is positive or negative.

The overflow flag is used in signed integer arithmetic when a positive value is too big or a negative value is too small to be represented in the register.

Control flags are utilized to control specific behavior in the processor. The DF flag which is the direction flag is used to control the way strings are handled by the processor. When set, string instructions automatically decrement memory addresses to get the next byte in the string. When cleared, string instructions automatically increment memory addresses to get the next byte in the string.

System flags are used to control OS level operations which should NEVER be modified by any respective program or application.

**TF**: Trap Flag

**IF**: Interrupt Enable Flag

**IOPL**: I/O Privilege Level Flag

**NT**: Nested Task Flag

**RF**: Resume Flag

**VM**: Virtual-8086 Mode Flag

**AC**: Alignment Check Flag

**VIF**: Virtual Interrupt Flag

**VIP**: Virtual Interrupt Pending Flag

**ID**: Identification Flag

The trap flag is set to enable single-step mode and when in this mode the processor performs only one instruction code at a time, waiting for a signal to perform the next instruction. This is essential when debugging.

The interrupt enable flag controls how the processor responds to signals received from external sources.

The I/O privilege field indicates the input-output privilege level of the currently running task and defines access levels for the input-output address space which must be less than or equal to the access level required to access the respective address space. In the case where it is not less than or equal to the access level required, any request to access the address space will be denied.

The nested task flag controls whether the currently running task is linked to the previously executed task and is used for chaining interrupted and called tasks.

The resume flag controls how the processor responds to exceptions when in debugging mode.

The VM flag indicates that the processor is operating in virtual-8086 mode instead of protected or real mode.

The alignment check flag is used in conjunction with the AM bit in the CR0 control register to enable alignment checking of memory references.

The virtual interrupt flag replicates the IF flag when the processor is operating in virtual mode.

The virtual interrupt pending flag is used when the processor is operating in virtual mode to indicate that n interrupt is pending.

The ID flag indicates whether the processor supports the CPUID instruction.

In our next tutorial we will discuss the stack.



