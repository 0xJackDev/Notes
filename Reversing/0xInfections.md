https://medium.com/@lelkins1313/malware-analysis-on-proxmox-b776240226c5
https://0xinfection.github.io/reversing/

Reverse Engineering is the process of Reversing An engineering process to see how things work.



We need to start with intro to x86.


Part 1: Goals


Essential to reverse engineering is the concept of modern malware analysis. Malware analysis is the understanding and examination of information necessary to respond to a network intrusion. 

The keys to the kingdom so to speak are rooted in the break-down of the respective suspected malware binary and how to find it on your network and contain it.



Upon full identification of the files required for deeper analysis, it is critical to develop signatures to detect malware infections throughout your network. There are two main types of signatures. Host based and network signatures

To begin with the concept of a host-based signature, we need to understand that these are utilized to find malicious code in a target machine. Host-based signatures are also referred to as indicators which can identify files created or edited by the infected code which can make hidden changes to a computers registry. This is quite in contrast with antivirus signatures because these concentrate on what the malware actually does rather than the make-up of the malware which makes them more effective in finding malware that can migrate or has been removed from the media.

In contrast, network signatures are used to find malicious code by examining network traffic. It is important to note such tools as WireShark and the like are often effective in such analysis.

Upon identification of these aforementioned signatures, the next step is to identify what the malware is actually doing.

So Host-based signatures is what the malware is actually doing say that it maintains persistence somewhere in the windows registry. Well then the host-based signature would be the act of modifying the registry to maintain persistence



Part 2 Techniques:


There are two basic techs that you can employ when analysis malware. The first being static and the other being dynamic analysis .



Static analysis uses software tools to examine the executable without running the actual decompiled instructions in assembly. We will not focus on this type right now however we will focus on actual disassembled binaries. 

Dynamic Analysis uses disassemblers and debuggers to analyze malware binaries while actually running them. The most popular is called IDA however there is many others such as Hopper Disaassembler, OllyDbg and more.




Part 4: x86 Assembly intro (AT&T VS INTEL)

The first question we must answer is what is x86 Assembly Language to which the answer is a family of backward-compatible Assembly Languages which provide compatibility back to the Intel 8000 series of microprocessors. x86 Assembly Languages are used to produce object code for the aforementioned series of processors. It uses mnemonics to represent the instructions that the CPU can execute.


Assembly language for x86 microprocessors work in conjunction with various operating systems. We will focus on Linux ASM utilizing Intel syntax in addition to learning how to program in C to which we will disassemble the source code and analyze the ASM.

x86 Assembly has two choices of syntax. The AT&T syntax was dominant in the Unix world since the OS was developed at AT&T and bell labs. In contract the Intel syntax was used for the original MS-DOS and windows platform. Also the x86 documentation mostly uses intel syntax 


For our purposes when we are debugging software we will see the Intel syntax most of the time. This is essential whether we are examining a windows binary in PE format or a linux binary in ELF format.

The main differences between the two is that in the AT&T syntax, the source comes before the destination and in the Intel syntax, the destination comes before the source. We will discuss this more in detail

We will focus on Linux Assembly 


We also focus on a 32-bit architecture as most malware is written for such to infect as many systems a s possible. 32 apps will work on 64 bits but 64 bit apps dont work on 32 bit systems.




Part 5: Binary Number System


In decimal, base 10, say we have the number 15 which means (1 x 10) + (5 x 1) = 15 therefore the 5 is the number times 1 and the 1 is that number times 10.

Binary works in a similar fashion however we are now referring to base 2. That same number in binary is 1111. To illustrate: 

![](https://0xinfection.github.io/reversing/imgs/1520526607781.jpg)




Part 6: Hexadecimal

Lets look at a simple table to see how hexadecimal compares to decimal.

![](https://0xinfection.github.io/reversing/imgs/1520241886257.jpg)


Every Hexadecimal number is 4 bits long. 

In hexadecimal, everything is dealt with in the power of 16. Therefore 42 in decimal is 2A in hexadecimal:



10 * 16 ^ 0 = 10

2 * 16 ^ 1 = 32

10 + 32 = 42 decimal => 2A hexadecimal
https://0xinfection.github.io/reversing/pages/part-6-hexadecimal-number-system.html





Part 7: Transistors and Memory

It is very important to fully understand hexadecimal and how to manually add and subtract them.


When we ask ourselves what is a computer made of one must go down as basic as one can get

Electronic computers are simply made out of transistor switches. Transistors are microscopic crystals of silicon that use electrical properties of silicone to act as switches. Modern computers have what we referred to as field-effect transistors.

Lets use an example of 3 pins. When an electrical voltage is applied to pin 1, current then flows between pins 2 and 3. When foltage is removed from the first pin it is also removed from pins 2 and 3.

When we zoom out a bit we see that there are also diodes and capacitors when taken together with the transistor switches we now have a memory cell. A memory cell keeps a minimum current flow to which when you put a small voltage on its input pin and a similar voltage on its select pin, a voltage will appear and remain on i ts output pin. The output voltage remains set in state until voltage is removed from the input pin in conjunction with the select pin

Why is this important? Very simply the presence of voltage indicates a binary 1 and the absence of voltage indicates binary 0. Therefore the memory cells holds a binary digit either 0 or 1.

In our next lesson we discuss bytes and words.




Part 8: Bytes, Words, Double Words etc.



Memory is measured in bytes a byte is 8 bits. two bytes are called a word and two words are called a double word or DWORD which is four bytes and a quad word is eight bytes (64-bit)


a byte is 8 bits and 2^8 power which is 256. The number of binary numbers in 8 bits in size is one of 256 values starting at 0 and going to 255


Every byte in a computer has its own unique address. Lets review the disassembled instructions for a simple hello world application i n linux by setting a breakpoint on the main function we will use the dgb debugger


lication in Linux by setting a breakpoint on the main function. We will use the GDB debugger:

![](https://0xinfection.github.io/reversing/imgs/1520519299095.jpg)

Don't worry if this does not make sense yet. The point of utilizing this example is to give you a sneak peek into our first program that we will examine in addition to learning about memory in a computer.

Below is an examination of the ESP register. Again, it is not critical that you understand what a register is or what ESP does. We simply want to see what a memory location looks like:

![](https://0xinfection.github.io/reversing/imgs/1520519298916.jpg) 

We see the memory location of 0xffffd040 which of course is in hexadecimal. We also see the value inside the ESP register which is 0xf7fac3dc which is also in hexadecimal.


It is important to understand that 0xffffd040 is 4 bytes and is a DWORD. As we learned in part 6 the hexadecimal number system, each hex digit is 4 bits long. In 0xffffd040 we  see 8 characters 8 x 4 = 32.

A computer program is nothing more than machine instructions stored in memory. A 32-bit CPU fetches a double word from a memory address. A double word is 4 bytes in a row which is read from memory and loaded into the CPU. As soon as it finishes executing, the CPU fetches the next machine instruction in memory from the instruction pointer.




Part 9: x86 basic architecture 

A computer application is simply a table of machine instruction stored in memory to which a binary numbers which make up the program are unique only in the way the CPU deals with them


The basic architecture is made up of a CPU, memory and I/O devices which are input/output devices which are all connected by a system bus as detailed below.

![](https://0xinfection.github.io/reversing/imgs/1520249055678.jpg)

Like this/


The CPU consists of 4 parts which are:

1) Control Unit - Retrieves and decodes instructions from the CPU and then storing and retrieving them to and from memory 
2) Execution Unit - Where the execution of fetching and retrieving instruction occurs
3) Registers - Internal CPU memory location used as quick data storage
4) Flags - indicate events when execution occurs
![](https://0xinfection.github.io/reversing/imgs/1520178351635.jpg)


we will discuss 32-bit x86 so therefor a 32 bit CPU fetches a dword from a specific address in memory and is read from memory and loaded into the CPU. at this point the CPU looks at binary pattern of bits within the double word and begins executing the procedure that the fetched machine instructions say to do.

Upon completion of execution an instruction the CPU goes to memory and fetches the next instruction in the sequence. The CPU has a register called EIP or instruction pointer that contains the address of the next instruction to be fetched from memory.
We can immediately see that if we can control the EIP we can alter the program to run OUR code.
The entire fetch and execute process is tied to the system clock which is a oscillator that emits square-wave pulses at precise intervals.
In our next tutorial we will dive deeper into the IA-32 Architecture with a discussion of the General-purpose Registers.

**IA-32** (short for "**Intel Architecture, 32-bit**"



Part 10: General-Purpose Registers

The general-purpose registers are used to temporarily store data as it is processed by the processor. we will focus on 32 bit. 
Each new version of general-purpose registers is created to be backward compatible with previous processors. This means that code utilizing 8-bit registers on the 8080 chips will still function on today's 64-bit chipset.

General-purpose registers can be used to hold any type of data to which some have acquired specific use which are used in programs. Lets review the 8 general-purpose registers in an IA-32 architecture.


**EAX**: Main register used in arithmetic calculations. Also known as accumulator, as it holds results of arithmetic operations and function return values.

**EBX**: The Base Register. Pointer to data in the DS segment. Used to store the base address of the program.

**ECX**: The Counter register is often used to hold a value representing the number of times a process is to be repeated. Used for loop and string operations.

**EDX**: A general purpose register. Additionally used for I/O operations. In addition will extend EAX to 64-bits.

**ESI**: Source Index register. Pointer to data in the segment pointed to by the DS register. Used as an offset address in string and array operations. It holds the address from where to read data.

**EDI**: Destination Index register. Pointer to data (or destination) in the segment pointed to by the ES register. Used as an offset address in string and array operations. It holds the implied write address of all string operations.

**EBP**: Base Pointer. Pointer to data on the stack (in the SS segment). It points to the bottom of the current stack frame. It is used to reference local variables.

**ESP**: Stack Pointer (in the SS segment). It points to the top of the current stack frame. It is used to reference local variables.

Keep in mind each of the above registers are 32-bit in length or 4 bytes in length. Each of the lower 2 bytes of the EAX, EBX, ECX, and EDX registers can be referenced by AX and then subdivided by the names AH, BH, CH and DH for high bytes and AL, BL, CL and DL for the low bytes which are 1 byte each.

In addition, the ESI, EDI, EBP and ESP can be referenced by their 16-bit equivalent which is SI, DI, BP, SP.

This can be a bit confusing to someone who has not studied computer engineering however let me illustrate in the table below:

![](https://0xinfection.github.io/reversing/imgs/1520145792750.jpg)

EAX would have AX as its 16-bit segment and then you can further subdivide AX into AL for the low 8 bits and AH for the high 8 bits. The same holds true for EBX, ECX and EDX as well. EBX would have BX as its 16-bit segment and then you can further subdivide BX into BL for the low 8 bits and BH for the high 8 bits. ECX would have CX as its 16-bit segment and then you can further subdivide CX into CL for the low 8 bits and CH for the high 8 bits. EDX would have DX as its 16-bit segment and then you can further subdivide DX into DL for the low 8 bits and DH for the high 8 bits.

ESI, EDI, EBP and ESP can be broken down into its 16-bit segments as follows:

![](https://0xinfection.github.io/reversing/imgs/1520613988729.jpg)

ESI would have SI as its 16-bit segment, EDI would have DI as its 16-bit segment, EBP would have BP as its 16-bit segment and ESP would have SP as its 16-bit segment.

In our next tutorial we will continue our discussion of the IA-32 Architecture with the Segment Registers.

Start at.

https://0xinfection.github.io/reversing/pages/part-11-segment-registers.html 


