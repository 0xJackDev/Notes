
type conversion is the process of changing the data type of a value to another value. For example changing strings to numbers or Booleans to numbers etc.  

A useful reason to do this is when we accept user input that is automatically gonna be a string. If we need to perform math operations to that we must convert it to a usable number first 

to convert something to a number use the Number() function for example

let age;

  
  

document.getElementById("submit").onclick = function(){

    age = document.getElementById("mytext").value;

    age = Number(age);

    age+=1;
    console.log(age);

}

this would print your age + 1. if i was to do this 

document.getElementById("submit").onclick = function(){

    age = document.getElementById("mytext").value;

    age+=1;

    console.log(age);

}

without converting it to a number it would add on the number 1 onto the string so lets say i inputted 22 it wouldn't be 23 instead 221. 



to convert to a string or a Boolean you can use the String(); Function or Boolean(); function respectively 



If you try to convert a String like the word "number" into a number value it would Return NaN which means Not a Number! 

If you convert a string to a Boolean, As long as there is Some value that isn't 0 then the Boolean will equal True. This is because Boolean like the code is either gonna be all 0s or a 1 and if its a 1 then its true 0 = false so if there's any type of data that's not NULL or a 0 then it will be true. The exception for this is even if you have a string with "0" inside of it IT will STILL BE TRUE since there is still data there inside of the string its registering. if you have a string with completely empty quotes "" it will equal False 


One reason you might want to convert a string to a Boolean is to see if user Input is Empty so you can make it like If this is false then you can tell the user they didnt type anything in. 

if you have a variable declared but not assigned a number it will Return NaN for number. Undefined string for string and False for Boolean. 