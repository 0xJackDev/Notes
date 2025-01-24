

Theres three problems with Memory.

1. What if theres not enough RAM on the system? Now this usually isnt a problem but back in the day it ALWAYS was so this is the real MAIN reason why virtual memory was developed because you needed to be able to run programs even without enough memory



Nowadays We almost never use virtual memory for this purpose as we have alot of RAM available now and accesses pagefiles for example is very slow so most devs wont do it.





2. Holes in our address space
Lets imagine we run a bunch of programs and then close them. Well once they are closed those chunks of memory that the program was loaded into is now just like Blank and it creates hole in our address space .



3. Programs writing over each other 
We also have problems with programs writing over each other. Because that each program can access anywhere in memory theoretically if two programs wrote to the same memory address it could be undefined behavior and possible crashing 



So what is virtual memory? and how does that solve our problems.


Well virtual memory is basically just indirection.

The idea is that we use the memory address  that the program uses and we map it to the real Physical Memory address. And by having this mapping going back in forth we can do alot of interesting things by controlling where the memory goes and how can use it.

We will talk about how it solves those problems and also 


about Page Tables and translation
Page tables is where we store the mapping and translation is how we actually do the mappings



Lets also talk about where we store these page tables and how to make these translation fast


We will finally talk about how Virtual memory interacts with CPU caches