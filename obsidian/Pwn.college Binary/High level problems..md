

C allows you to access variables out of bounds  in a array. ![[Screenshot 2025-01-08 213716.png]]





The stack everything is jumbled together. 

If you say code an array like 


int a[3] = {1,2,3};
a[10] = 0x41; 

This would allow you to overwrite stuff 7 Bytes to the right of the arrays actual bounds.


All data is stored together and treated the exact same. Instructions. Function names, Pointers anything. 


You can do alot of this. If you overwrite control data such as a return address you can use this to redirect control flow elsewhere. I.e to your malicious function or elsewhere in the code which allows you to bypass security checks.


C also doesnt clean up after your code runs. Meaning all those variables. Functions nad everything in memory doesnt get deleted UNLESS you tell it to. Same as C will not initalize anything without being told to



Defensive programming is important for example if you pas thru a null terminator to a  input that is a string it may Break da program