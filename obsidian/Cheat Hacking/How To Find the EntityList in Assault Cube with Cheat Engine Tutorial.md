


Anytime you see a memory instruction like this mov eax,[edi+esi*4] You will know because of the *  your on the right track to find the entity list. This is because The entity list in assault cube is an array of entity pointers And each pointer is 4 bytes  So the reason we know this instruction is something to do with the entity list is hey 4 is the size of a pointer. esi is the element iterator of the array we are in for example array[iterator] and then edi is the address of the player array. So we take the address of the player array.

So if we take the address of the player array and add + 0x4 that will give us the address of the first element of the array. 



Also its useful that when you see Memory in a certain range. Most likely other variables will be inside that range too. THis can help you narrow down which one is most likely to be the correct memory address


This is the instruction above the compare with the name. it is Loading an affective address into the esi register. Which it is getting from the Value stored at EDI + an offset of 225.
lea esi,[edi+00000225]



Also make sure that you are in the Main part of the game and not the menu or anytjing as this can create undefined behavior or just simply some code hasnt loaded so some isnt be shown



https://www.youtube.com/watch?v=TCu0qSivXUc


This is a really really good video! On utizing offsets 