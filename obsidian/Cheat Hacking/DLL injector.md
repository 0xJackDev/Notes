
In theory a DLL injector is pretty simple all you must do Is find the Process ID of the Game you want to inject your DLL into and then from the procId of that process. Then Use the OpenProcess() function with the games procID.

The next step involves creating a remote thread in the target process using CreateRemoteTHreat. The Thread will call loadlibraryA and pass the location where we stored the DLL path and close the thread and process handles