

The reason we do a trampoline hook is so that we dont keep returning to the same stolen jmp and keep running our Stolen code and never jump back to the games stack

![[Screenshot 2024-12-06 170654.png]]



Instead of having our code run inside of a while loop we are instead going to hook a function which runs every frame of the game. In this case it will be OpenGL so we are going to hook into a OpenGL function 


If we drag Assault cube into Ida Pro and look on the Imports table we will see they Import a Function From OpenGL which is. So instead of having a seperate thread running we will hook a function



The most annoying here was to find the actual EXE of the game. I did this by finding the .bat start file which has

start bin_win32\ac_client.exe "--home=?MYDOCUMENTS?\AssaultCube_v1.2" --init %1 %2 %3 %4 %5

telling me that the exe is stored at C:\Program Files (x86)\AssaultCube\bin_win32. Then i can Decompile that



What is A SwapBuffer? 
SwapBuffers is an OpenGL function that allows double buffereing. ![[Screenshot 2024-12-07 114547.png]]


So we hook SwapBuffers so that we can draw an overlay on the BackBuffer