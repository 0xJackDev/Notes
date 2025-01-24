

Once you find a memory address in which you would like to find a pointer to. You will need to find which offset it uses in order to find the enity object.  so to find the offset you need to see what accesses or what write to this memory address and use deducation. In assault cube its easy as almost all of them add by F8 besides the one that adds with 04. 


the ESI register alot of the times is the address of the entity object, This is not guaranteed but this is typical in most games 

In the case of assault cube and in this instance of the game the ESI address held the value 02B5A418 in all actions where ESI is called, therefor using deduction this is a needed value and I can assume this is the Entity object address.


An object is an instance of a class.

The next thing your gonna wanna do is look at the structure of the Entity object address, as this is what all of the other variables like Health for example are gonna be using to Add their offset to to get their own address



We need to find a Static address / Pointer 

This is going to relative to a Module/ Exe,dll That is always loaded into the same place in memory. 

So we wanna find a pointer to our entity object


So to do this we are gonna paste the value of the Enity Object address into cheat engine and do a scan.