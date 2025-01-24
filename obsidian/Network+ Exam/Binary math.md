
A bit is a 1 or a 0


In these notes we will be learning how to manually convert to binary



when we put 8 of these its together its called a byte. This is often called a octet because of the 8 bits in networking. 

To be able to do our Conversion we must make a binary-to-decimal conversion chart 




Remember binary uses Multiples of 2 so every time you move you move a 0 to the right it will double. so for example

0 = 0
10 = 2
100 = 4
1000 = 8 
1000 0  = 16
1000 00 = 32
1000 000 = 64
1000 0000 = 128

This is a example of a chart, I only use 8 but when doing ip subnetting you may have to look at longer charts. But the majority of what you are working with will be 8 bits made into a byte 

Lets say we have a byte 
![[Screenshot 2024-07-05 210424.png]]





For every place there's a binary 1 we are gonna bring down the decimal value, and for everyone that there's a 0 we bring down a 0 and then add all of the numbers together
For example the binary 
1001 1000
=
144



Decimal to binary conversion 


If we want to take the decimal value of 154 and convert it to binary we will follow the same conversion chart

So we dont know what those binary equivalents are yet. The decimal 154 has a single combination of 1s and 0s it could be . So what we will do is start with the largest number that we can fill which is 128. so 
1000 0000 
is the binary number but we still have 26 left over, Well whats the largest number that 26 can fill?, 16 so now we have.
1001 0000
with 10 leftover so we do the largest we can which is 8 
1001 1000
so now we have two left over
1001 1010
So 154 = 1001 1010. 

Basically you just put a 1 in the largest number that the decimal number could fill subtract it and keep going until you reach a value of 0 and then that is the Binary number 





You can write out charts that deal with more complicated stuff, ![[Screenshot 2024-07-05 211321.png]]



Extending the math is really just powers of twos. ![[Screenshot 2024-07-05 211350.png]]