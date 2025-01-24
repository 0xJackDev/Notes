


THere is a couple neat features in the topleft in the process tab, You can view Process information which will show you all Modules AKA Dlls and EXES that are loaded and their addresses and size and also the memory sections. There is also a memory scanner like cheat engine But the main thing we use it for is reversing strctures.

So lets look at the Entity Object Pointer. Which Points to the LocalPlayerObject In memory 


The syntax to look at the pointer in REclass is as follows

[<ac_client.exe>+10F4F4]

<> around the Exectuable and [] which says to deference it. 


Reclass shows Blocks in Multiple types for example on the first one is a float. The second is an integer and the third is the hexadecimal representation So when looking at it. Logically you can describe and see which one it is most likely. The hexadecimal address if it points to a memory address that would make sense well that means that is a pointer



At the begging we see something about world ent. This is a Virtual Function Table. If we Change this type to a V table we can expand it and see all of the seperate functions inside of there. So it will derefernce the pointer and look at the functions inside of the Array. And now if we open up these functions we can see the actual assembly instructions


Then by looking at the logic of what happens when we do stuff 



Remember that what you see if Just reclass putting back together what these variable sizes are. Specifcally for Char arrays. There may be the wrong amount of letters. Since at first all of the things are in 4 byte blocks. Lets say you have an array of chars that takes of 16 bytes. Well you would have to change the data type from the begging of the char array change the type to a ASCII text UTF-8 and inside of [2] which it will default to do [16] saying it takes up 16 bytes An important part of this is getting used to setting the padding as it wont always be 4 bytes. 

ALSO AFTER U SET THE 16 byte char array all the bytes after that wont be four byte aligned so we want to make it so that they are. So just click buttons until you find that all of them are increasing by 4 sequentially. showing that 4 bytes are the padding.

ALSO REMEMBER STRINGS END WITH a NULL TERMINATOR THAT COOUNTS AS A CHAR 



If you see the Current Weapon Pointer You can change the Data type to a pointer which will point ot a instance of the class weapon


The real Magic of realclass is when you go to the topleft in project and Generate C++ code. Now it will give us the structure we can use directly in our code


Make sure your using the Latest version of C++




Now theres another method called auto padding. The above works good for games that offsets dont update often but for a game like CSGO this isnt good as they update every week. 


Review This video about questions about using the code internally https://www.youtube.com/watch?v=vQb21RM9-5M