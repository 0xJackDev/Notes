

What is a Detour?

The word detour describes the act of changing the assembly instructions to a jump to a different location, essentially re-directing the flow of execution. Typically you are doing this to detour into a memory region where your own code exists


## Mid function hooking
A detour is sometimes refered to as a mid function hook, the only caveat being that if you detour the first byte of a function, then this is not a mid funciton hook. But placing your detour at the first byte of a function is bad practice as that is easily detectable by game anti-cheat, which is why mid function hook is less detectable as it is less likely the anticheat checks every byte. 


## External Detouring / Hooking
Typically you will do this by using WriteProcessMemory to write your code into the target process, Then you use WPM in the same way to change the existing code to jump into your code. External hooking is more complicated because you must write shellcode into the target process. Internally you can do it quite easy. But externally you have to turn your assembly into bytes and write it to a process as shellcode. When your internal its much easier you dont need to play with assembly as much.


0FFFFFFFFFFFFFFFFh
## Stolen bytes
The bytes you overwite when writing your detour to memory are refered to as stolen bytes, it is important that you know how many bytes you overwrote and you must execute these after you perform your detour or else the stack/registers will be corrupted. The number of bytes isnt always the same too, lets say you overwrite an instruction which is 8 bytes, but your detour your writing is only 5 bytes. In this case you want to copy all 8 bytes for the stolen bytes. As you cant execute 75% of an instruction. 

You must copy the stolen bytes and execute them after your own code executes to ensure you dont crash the program.



## Code caves 

A code cave is a portion of the target process memory which is not used by the process. Typically we are referring to memory which is allocated but contains nothing that the process requires to execute. When using a detour, you can write your code into this memory without having to allocate memory. By not having to allocate memory you are being less "noisy". If you are using a codecave, the memory page must have execute permissions. You can modify these memory protection constants with VirtualProtect or VirtualProtectEx



https://www.youtube.com/watch?v=jTl3MFVKSUM


Essentially all a hook does is redirect the programs flow 



0x90 is the NOP instruction in hexcode

