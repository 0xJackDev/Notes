

We will be writing to proccess memory of our own executable file at 
C:\dev\Learn 2 hack\x64\Release\Learn 2 hack.exe



Read Proccess memory
```
#include <Windows.h>
#include <iostream>
#include <string>



int main() {
	int intRead{ 0 };
	DWORD pid = 101388;
	HANDLE hProccess = OpenProcess(PROCESS_ALL_ACCESS, FALSE, pid);
	uintptr_t memoryAddress = 0x7CC14FFD80;
	ReadProcessMemory(hProccess, (LPCVOID)memoryAddress, &intRead, sizeof(int), NULL);

	std::cout << intRead;


}
```




WriteProccessMemory
```
#include <Windows.h>
#include <iostream>
#include <string>



int main() {
	int intToWrite{ 987654 };
	DWORD pid = 92716;
	HANDLE hProccess = OpenProcess(PROCESS_ALL_ACCESS, FALSE, pid);
	uintptr_t memoryAddress = 0xE74C12F7F0;
	int checkError = WriteProcessMemory(hProccess, (LPVOID)memoryAddress, &intToWrite, sizeof(int), NULL);
	if (checkError != 0) {
		std::cout << "Overwritten Successfully";

	}
	else {
		std::cout << "Write ProccessMemory Failed With error code = " << std::dec << GetLastError() << std::endl;
	}


}
```


