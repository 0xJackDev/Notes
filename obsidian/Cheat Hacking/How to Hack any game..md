

What our code will do. 

Loop through all Processes on system and get Game process ID. we are then going to use open process to get a handle to a certain memory access permission and then use GetModuleBaseAddress to find a PE then use FindDMAAddy to calculate the Value of a multi-level pointer.  

We start by finding the memory address of Ammo in shotgun
0108A628 = Value = 5 
We see 004637E9 - FF 0E  - dec [esi] when we check what accesses this. Telling us that there is an offset of 0.  We then scan for the memory address of 0108A628 to see anything that has a value that is that and find 0108193C.
0108193C -> 0108A628 + 0 = 0108A628 
```
Since we know 0108193C has the value of 0108A628 The base ptr. We check what scans this and get mov ecx,[esi+14] telling us the offset is 14. and since it is in ESI we go into the ESI register and see that the value stored is 01081928. Then we do a scan for 01081928 and see what has a value of that and find multiple addresses. We only grab the ones that start with 0108 and from there in order to find the real one we run Find out what accesses on each one and which ever one responds to us shooting our gun is the real. I narrow it down and find two that both respond. 0108A838 and 0108A86C. Im gonna go with 0108A86C as it has a offset and the other doesnt
```
0108A86C -> 01081928 + 14 = 0108193C 

I find offset, look in Esi find 01081928 do a search and find 0108A86C
0108A86C -> 01081928 + 384 = 0108A86C 
static base addr -> 01081928 + 384 = 0108A86C



if you see something in brakets [] like dec [esi] that means it is dereferencing esi and then getting the value inside of it to perform operations on 



0108A638 = Value = 20 
01081834 -> 0108A638 + 0 = 0108A638 
0108A86C -> 01081820 + 14 = 01081834 
ac_client.exe+10F4F4 -> 0108A4E8 + 374 = 0108A86C 



proc.h
```
#pragma once

#include <vector>
#include <Windows.h>
#include <TlHelp32.h>


DWORD GetProcId(const wchar_t* procName);

uintptr_t GetModuleBaseAddress(DWORD procId, const wchar_t* modName);

uintptr_t FindDMAAddy(HANDLE hProc, uintptr_t ptr, std::vector<unsigned int> offsets);


class proc
{
};


```


proc.cpp
```
#include "proc.h"



DWORD GetProcId(const wchar_t* procName) {
	DWORD procId{ 0 };
	HANDLE hSnap = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS, 0);
	if (hSnap != INVALID_HANDLE_VALUE) {
		PROCESSENTRY32 procEntry;
		procEntry.dwSize = sizeof(procEntry);

		if(Process32First(hSnap, &procEntry))
		{


			do 
			{
			if (!_wcsicmp(procEntry.szExeFile, procName))
				{
					procId = procEntry.th32ProcessID;
					break;
				}

			} while (Process32Next(hSnap, &procEntry));
		}
	}
	CloseHandle(hSnap);
	return procId;
}

uintptr_t GetModuleBaseAddress(DWORD procId, const wchar_t* modName) {
	uintptr_t modBaseAddr = 0;
	HANDLE hSnap = CreateToolhelp32Snapshot(TH32CS_SNAPMODULE | TH32CS_SNAPMODULE32, procId);
	if (hSnap != INVALID_HANDLE_VALUE)
	{
		MODULEENTRY32 modEntry;
		modEntry.dwSize = sizeof(modEntry);
		if (Module32First(hSnap, &modEntry))
		{
			do
			{
				if (!_wcsicmp(modEntry.szModule, modName))
				{
					modBaseAddr = (uintptr_t)modEntry.modBaseAddr;
					break;
				}
			}while (Module32Next(hSnap, &modEntry));
		}
	}
	CloseHandle(hSnap);
	return modBaseAddr;
}

uintptr_t FindDMAAddy(HANDLE hProc, uintptr_t ptr, std::vector<unsigned int> offsets)
{
	uintptr_t addr = ptr;
	for (unsigned int i = 0; i < offsets.size(); ++i)
	{
		ReadProcessMemory(hProc, (BYTE*)addr, &addr, sizeof(addr), 0);
		addr += offsets[i];
	}
	return addr;
}

```


HackAnyGame.cpp

```
#include <iostream>
#include "proc.h"
#include <vector>
#include <Windows.h>





int main()
{
	//Get ProcId 
	DWORD procId = GetProcId(L"ac_client.exe");

	//GetModuleBaseAddr
	uintptr_t moduleBase = GetModuleBaseAddress(procId, L"ac_client.exe");

	//Get Handle to Process with all access
	HANDLE hProcess = 0;
	hProcess = OpenProcess(PROCESS_ALL_ACCESS, NULL, procId);

	//Resolve Base address of pointer chain
	uintptr_t dynamicPtrBaseAddr = moduleBase + 0x10f4f4;

	std::cout << "Dynamic ptr Base addr = " << "0x" << std::hex << dynamicPtrBaseAddr << std::endl;

	//Resolve ammo pointer chain btw its unsigned as a memory addr will never be negative
	std::vector<unsigned int> ammoOffsets = { 0x374, 0x14, 0x0 };
	uintptr_t ammoAddr = FindDMAAddy(hProcess, dynamicPtrBaseAddr, ammoOffsets);

	std::cout << "ammo addr = " << "0x" << std::hex << ammoAddr << std::endl;

	//read ammo value
	int ammoValue = 0;
	ReadProcessMemory(hProcess, (BYTE*)ammoAddr, &ammoValue, sizeof(ammoValue), nullptr);
	std::cout << "Current ammo = " << std::dec << ammoValue << std::endl;

	// Write Ammo value
	int newAmmo = 1337;
	WriteProcessMemory(hProcess, (BYTE*)ammoAddr, &newAmmo, sizeof(newAmmo), nullptr);

	// Read again
	ReadProcessMemory(hProcess, (BYTE*)ammoAddr, &ammoValue, sizeof(ammoValue), nullptr);}
	std::cout << "Current ammo = " << std::dec << ammoValue << std::endl;

	getchar();
	return 0;


}


```