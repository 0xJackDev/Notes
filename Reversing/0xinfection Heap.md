
Our next step in the basic malware reverse engineering section focuses on the Heap. Keep in mind the stack grows downward and the heap grows upward. It is very important to understand this concept.

![](https://0xinfection.github.io/reversing/imgs/1520241941781.jpg)

The heap is a region of your computers memory that is not managed automatically for your, and is not as tightly managed by the CPU. it is a free-floating region of memory and is larger than the stack allocation of memory.

To allocate memory on the heap you must use malloc() or calloc() which are built in C function. Once you have allocated memory on the heap you are responsible for freeing it using free() to de-allocate that memory once you dont need those variables anymore

if you dont do this your program will have what is known as a memory leak. That is memory on the heap will be set aside and wont be available to other processes that need it.


unline the stack the heap does not have size restriction on variable size. the only thing that would limit the heap is the physical limitations of your computer. Heap memory however is slightly slower to be read from and written to, because you have to use pointer to access memory on the heap. When we dive into our C tutorial series we demo this

Unlike the stack variables on the heap are accessible by ANY function aka GLOBAL anywhere in your program. Heap variables are essentially global in scope

If you need to allocate a large block of memory for something like a struct or a large array and you need to keep that variable around for a good duration of the program to which must be accessed globally, then you should choose the heap for this purpose. If you need variables like arrays and structs that can change size dynamically such as arrays that can grow or shrink as needed, then you will likely need to allocate them on the heap, and use dynamic memory allocation functions like **malloc()**, **calloc()**, **realloc()** and **free()** to manage that memory manually.

The next step is to dive into programming C in the Linux environment where we step-by-step disassemble each C program so in effect you will be learning both C programming and Assembly so that you can progress your skills in Malware Analysis and Reverse Engineering.

I look forward to seeing you all next week when we take a comprehensive step-by-step tutorial on how to install Linux on your current computer using the FREE Virtual Box software tool.



