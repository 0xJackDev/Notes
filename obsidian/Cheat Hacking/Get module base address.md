

How do you get the base address of a process or module in C++, well we use dwGetModuleBaseAddress is the function in WinApi that does this. It has been used for many years and we will improve upon it in this turotial by creating a function that simply named GetModuleBaseAddress. This module base address tutorial will teach you how to get the address of any module and how to use simple C++ versions.


### **What will you learn?**​

- How to find the module base address in Cheat Engine
- How to find the base address of a module using C++
- How to navigate through the module list
- How to obtain a list of modules for a specified process

### **Why do you need these skills?**​

Why would you need to know the base address of a module? Everything you do in game hacking will involve relative offsets, the module will not always be loaded into the same base address. To compensate for this you are required to find the base address of the module at run time using the Windows API. The [ToolHelp32](https://learn.microsoft.com/en-us/windows/win32/api/tlhelp32/) library provides us the functionality needed to loop through the modules and get their base addresses.

### **What is a module?**​

An .EXE or .DLL file (both are Portable Executable files) are referred to as _**binaries**_ when they are on disk but they are called _**modules**_ when loaded into memory.

### **Why don't modules have the same address every time?**​
In the PE header for each binary, there is a field called **_ImageBase_** which defines the address it should be loaded. But what happens when another module is already in that location? Then the Windows loader will find a different address for it, this is called DLL re-location. That's why it's referred to as the **_preferred_** image base.


### **What about ASLR?**​

You can imagine that exploiting vulnerabilities is quite simple when the things you're trying to exploit are in the same address on every computer, every time the program runs, right? That's why Microsoft added Address Space Layout Randomization as a security feature. With ASLR enabled, the address where a module is loaded is randomized. But in reality this is a very poor security feature, getting the address at runtime is quite simple as we will show.





### **.EXE vs .DLL Preferred Image Base**​

When an EXE is loaded, the virtual address space of the process is empty, so it can always load into it's preferred image base address.  
The only time an .exe isn't loaded into the **_PreferredImageBase_** is when ASLR is enabled on the OS and the DynamicBase flag is set to enable the OS to randomize the virtual address of the module.  
  
But none of this really matters, ASLR is standard procedure now so we just assume it's enabled and use our function to ensure we get the right address.



## Visual Example Using Cheat Engine​

To view all the modules loaded by a process using Cheat Engine:  

1. Click Memory View
2. Click Tools
3. Click Dissect PE Headers

![[Pasted image 20240924201434.png]]

  
  
In the resulting window click on any DLL or .EXE and then expand _PE Header_ to show this:  

![[Pasted image 20240924201444.png]]

  
#3 is the preferred image base from the PE header and #4 is the current base address. They are the same in this example because ASLR is disabled and it's an EXE.  
  
**Common mistake:** Make sure you click "info" each time you select a new module or it won't load the new results.

## **Our GetModuleBaseAddress Function**​

There are actually multiple different ways to get the base address. The Windows API function named **CreateToolhelp32Snapshot** is the easiest and learning it will enable you to use this entire library as most of the functions work in the same way.  
  

### **Why not just use the old dwGetModuleBaseAddress?**​

The old function uses DWORD so it only supports x86. Our function uses uintptr_t which will resolve to a x86 or x64 address depending what architecture you build for. This makes it work on both, so you only need one function.



C++ GetModuleBaseAddress function
```
uintptr_t GetModuleBaseAddress(DWORD procId, wchar_t* modName)
{
    //initialize to zero for error checking
    uintptr_t modBaseAddr = 0;

    //get a handle to a snapshot of all modules
    HANDLE hSnap = CreateToolhelp32Snapshot(TH32CS_SNAPMODULE | TH32CS_SNAPMODULE32, procId);

    //check if it's valid
    if (hSnap != INVALID_HANDLE_VALUE)
    {
        //this struct holds the actual module information
        MODULEENTRY32 modEntry;

        //this is required for the function to work
        modEntry.dwSize = sizeof(modEntry);

        //If a module exists, get it's entry
        if (Module32First(hSnap, &modEntry))
        {
            //loop through the modules
            do
            {
                //compare the module name against ours
                if (!_wcsicmp(modEntry.szModule, modName))
                {
                    //copy the base address and break out of the loop
                    modBaseAddr = (uintptr_t)modEntry.modBaseAddr;
                    break;
                }

                //each iteration we grab the next module entry
            } while (Module32Next(hSnap, &modEntry));
        }
    }

    //free the handle
    CloseHandle(hSnap);
    return modBaseAddr;
}
```



How to call the function above

```
    uintptr_t clientDLLBaseAddr = GetModuleBaseAddress(ProcId, L"client.dll");

```


## How does it work?
CreateToolhelp32Snapshot returns a handle to a snapshot which contains all the information for all the loaded modules in the designated process. You then iterate through all the loaded modules using Module32First and Module32Next. During iterations it compares the process name to find the correct module and returns the correct module addr, if not found it returns 0

You input the ProcessId and the name of the module and it outputs the address of the module. In order for your project to function it must be set to UNICODE
### **But wait, we're missing ProcId?**​

This is just the Process ID. Don't worry, the `GetProcID()` function will be taught to you in the video later.

### **Unicode vs MBCS vs TCHAR**​

Notice the `wchar_t* modName`?  
wchar_t means we're using unicode so you must pass in a unicode string which we do using the L macro to mark our literal string as unicode:  
`L"client.dll"`  
  
If you want to use MBCS use `char*` instead of `wchar_t*`.  
If you want to use TCHAR change to `TCHAR*`  
  
You will also have to change `_wcsicmp` to a comparable string compare function: `_stricmp` or `_tcsicmp`  
  
Keep in mind that using Unicode is standard procedure in 2022, we try to do that in all our tutorials but some use regular ANSI/ASCII encoding.



### How to Get Module Base Address Internally?​

Getting a module base address in an internal hack is much easier, you just call GetModuleHandle and you're done.  

C++:Copy

```cpp
uintptr_t clientDLLBaseAddr = (uintptr_t)GetModuleHandle(L"client.dll");
```



