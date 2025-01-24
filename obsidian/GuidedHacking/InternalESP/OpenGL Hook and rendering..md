

Look at the [Trampoline hooks.]  to see how we hook into the Opengl SwapBuffer function.




We need to Grab the SwapBuffers hook which is


```
bool mem::Detour32(BYTE* src, BYTE* dst, const uintptr_t len) {
	std::cout << "Hooked" << std::endl;
	if (len < 5) return 0; // The minimum size for a jump is 5 bytes so  this is to protect us from overwriting something that cant be

	DWORD curProtection; 
	VirtualProtect(src, len, PAGE_EXECUTE_READWRITE, &curProtection); // We need to call Virtual Protect since the pages of memory we are gonna be hooking into only have read permissions we need to make the permissions so we can change da memory

	uintptr_t relativeAddress = (dst - src) - 5; // Calculate Relative address from the Src to the destination 

	*src = 0xE9; // Change the src byte to the hexadecimal code for jmp. which is 0xE9

	*(uintptr_t*)(src + 1) = relativeAddress; // Typecast to uintptr* then dereference. This writes our relative address which we are jumping to.

	VirtualProtect(src, len, curProtection, &curProtection); // Return the Permissions of memory page back to normal 
	return true;

	
}
BYTE* mem::TrampHook32(BYTE* src, BYTE* dst, const uintptr_t len) {

	if (len > 5) return 0; // Protection


	// Create Gateway and cast to BYTE pointer This is standard for creating Codepages you will bne executing.
	BYTE* gateway = (BYTE*)VirtualAlloc(0, len, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);


	// Write the stolen Bytes to the gateway using memcpy
	memcpy_s(gateway, len, src, len);

	// Get the Gateway to destination address
	uintptr_t gatewayRelativeAddr = src - gateway - 5;


	// add jmp opcode to end of gateway
	*(gateway + len) = 0xE9;


	// Write address of gateway to jmp
	*(uintptr_t*)((uintptr_t)(gateway + len + 1)) = gatewayRelativeAddr;

	// Perform the detour
	Detour32(src, dst, len);


	// Return gateway This does the jump back into the Games function
	return gateway;

}
```



We also need all the function related to GL drawing. This requires the OpenGL32.lib to be included into the project as it allows us to include the GL.h header which includes all the functions we need to draw.

you can just add it in source code by doing #pragma comment (lib, "opengl32.lib")


There is some api hooking way to hook into openGL easily but every game is gonna be different. 

our project is Internal_hack


Drawing to the screen should be the last thing we do


Debug internal DLLs by attaching to process

