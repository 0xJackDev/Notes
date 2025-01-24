

Lets say I want to change the value of a variable called student by adding 2 we would do 


let student = 30;

student = student + 2;

console.log(student);

which logs 2 to the console. 

this goes for division/ subtraction multiplacation and addition .


in order to do exponents it is represented by ** or double asterisks lets say i wanted to put student to the second power.

let student = 30;

student = student ** 2;

console.log(student);

This would log 900 to the console as that's 30 to the second power. 



The modulus operator gives the reminder of any division this is %. If it is anything other then 0 that means there is a reminder. This is is VERY useful for checking if something is a even or odd number.

let student = 30;

student = student % 2;

console.log(student);

this logs 0 since 30 divides by 2 evenly if we were to say use 31 then 1 would be logged. 



To increase students by 1 we could also do

students += 1; 

which would make students 31.


you can do the same thing with subtraction like -=. 

This goes for all operators. 



There is also the increment and decrement operator to add 1 to student you can also do

student++;

or to remove 1 
student--; 


the operator precendence goes 

1. Parenthesis 
2. Exponents 
3. Multiplication and division and modulo
4. Addition and subtraction. 
Going from left to right.


let result = 1 + 2 * 3 + 4 ** 2;

console.log(result);

this will log 23. Lets walk through step by step .

first we do  4 ** 2 which = 16 so now we have

1 + 2 * 3 + 16;

so we do 3 * 3 and get 6 so now we have 

1 + 6 + 16 which = 23



