
Do you have a multilevel pointer from Cheat Engine that you're trying to use in a C++ hack? Our FindDMAAddy function is exactly what you need. Learn how to use the FindDMAAddy function to follow the pointer chain and get the dynamic address of the variable you need using this article.


Find Dynamic Memory allocation address function was created more than 10 years ago, published on MPGU anmd primarily promoted by Fleep, the orignal owner of GH who gave it its iconic name. FindDMAADDY automates the parsing of multi level pointers so you dont have to do it manually. Works on x86 and x64



By walking this pointer chain your actually just replicating the actual logic the game uses the access that variable. When you find a pointer in cheat engine what you finding is a path from one address to a nother using pointers and relative offsets. This is how computers locate and act on data stored in memory. Its not magic!


1. Applications are made memory efficient by dynamically allocating objects only when needed. Pointers are used to point at these objects so you can access them via pointers. 
2. Classes can contain member variables that are pointers, specifically pointers to other objects in memory

A simple Example of real life multi-level pointer logic

```
class PlayerClass
{
	public:
		int health;
		int armor;
		char* name;
}

// Creating a pointer capable of pointing at playerclass object
PlayerClass* localPlayer;

// Creating a new dynamic Playerclass object and making our pointer point at it.
localPlayer = new PlayerClass();



```



Lets explain shortly;


Class Playerclass
Health is offset 0x0 and armor is offset 0x4, because an integer is only a 4 byte variable in this example. The name variable is a pointer to a char array at offset 0x8 and this char array actually contains the ASCII letters of the name


PlayerClass* Localplayer
Playerclass is the name of the class, the * tells the compiler that this is a pointer to an object of the type PlayerClass and its identifier is localPlayer. In this example it is not initalized meaning no memory has been allocated for it so technically it is a dangling pointer rn because it hasnt been initalized to anything. 



localplayer = new PlayeClass
When the player starts the a game the localPlayer object is allocated a random spot in memory on the heap and the pointer is assigned the address of the object. So our pointer now points at our dynamic object



in this example the address of the local player object wouldnt be cosistent and you would need to find a pointer to it. If you used Cheat engines "Find what accesses this address" or the pointer scanner on the name variable you would find a multi level pointer where the baseAddress is the address of localPlayer and offset 0x8 leads you to the name pointer which when de-referenced gives you the value of the char array containing name.



it simply uses the same logic that assembly code does to find the address of the variable. In the source code of this application if you wanted to use the name variable you would use the pointer arrow -> (called the structure de-reference operator) like t his:
localPlayer -> name


When the compiler compiles this code into assembly the logic it creates basically looks like:


1. Dererence the localPlayer pointer to get the dynamic address of the object
2. Add the offset 0x8 to the name pointer
3. Dereference the name pointer to get the dynamic address of char array.


How to do it in C++, well we can manually do it for every pointer by doing something like
```

ReadProcessMemory(handle, (LPVOID)pointeraddress, &newpointeraddress, sizeof(newpointeraddress), NULL); 
ReadProcessMemory(handle, (LPVOID)(newpointeraddress+ offset[0]), &newpointeraddress, sizeof(newpointeraddress), NULL);
ReadProcessMemory(handle, (LPVOID)(newpointeraddress + offset[1]), &newpointeraddress, sizeof(newpointeraddress), NULL); 
ReadProcessMemory(handle, (LPVOID)(newpointeraddress + offset[2]), &newpointeraddress, sizeof(newpointeraddress), NULL);

```



But that wastes your time especially doing that for every pointer, instead make a function that does it for you. We emulate the logic in our FindDMA addy function.



## FInd DMAaddy source code. 




## EXTERNAL FUNCTION
Use this in external cheats it uses Read ProcessMemory and requires process handle (use OpenProcess to get handle)

```
uintptr_t FindDMAAddy(HANDLE hProc, uintptr_t ptr, std::vector<unsigned int> offsets) 
{
uintptr_t addr = ptr; 
for (unsigned int i = 0; i < offsets.size(); ++i) 
{ 
	ReadProcessMemory(hProc, (BYTE*)addr, &addr, sizeof(addr), 0); 
	addr += offsets[i]; 
} 
	return addr; }
```


## Get current weapons ammo address using our example

```cpp
uintptr_t ammoAddr = FindDMAAddy(hProcess, dynamicPtrBaseAddr, { 0x374, 0x14, 0x0 });
```

At this pointer you can use ReadProcessMemory to read the value at the address of ammoAddr to or overwrite it with WriteProcessMemory.




## Internal Function

When you are internal (injected DLL or shellcode) you dont need to use ReadProcmem cause you have direct Memory access

```
uintptr_t FindDMAAddy(uintptr_t ptr, std::vector<unsigned int> offsets) 
{
	uintptr_t addr = ptr; 
	for (unsigned int i = 0; i < offsets.size() ; ++i) 
	{ 
	addr = *(uintptr_t*)addr; 
	addr += offsets[i]; 
	} 
	return addr; }
```



If you get confused on Multilevel Pointers read this

https://guidedhacking.com/threads/c-what-is-a-multi-level-pointer-tutorial.11881/


