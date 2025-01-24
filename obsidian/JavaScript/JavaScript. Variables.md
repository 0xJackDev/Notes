
A variable is a container that stores a value.

There is two things you must do to a variable. 

1. Declaration, this is where you declare that a variable exists and the name of the variable without setting a value for example in JavaScript you do let *variable name*; 
		let x; declares a variable named x 
1. Assignment. This is where you assign a variable. for example if you wanted to assign a variable named x to the value of 100 you would do x = 100;



say i wanted to change a element named who text content to display the value of a variable x I could do. 
```
	document.getElementById("who").textContent = x
```




There is a few different data types in javascript. 


There is Numbers which includes integers and floats any number is gonna be a Number class.

In order to insert a variable into a string use ${*var_name*} for example to log the age of user you can do.

console.log(`Your age is ${age}`);


Technically you could also do console.log("Your age is",age); and it would work the same but this is consider bad practice has every time you want to introduce a varaible inside of a string you must end "" and open up a new pair. 



```
document.getElementById("who").textContent = `Hi I see your age is ${age}`;

```



if you wanna display the datatype of a variable precede the variable with the *typeof* keyword

for example

age = 22;
console.log(typeof age);

This would output *number* to the console.



There is also a string datatype. to create a string either use single quotes or double quotes or 


let name = "Jack"

let food = "pizza";


console.log(`Hi ${name} your favorite food is ${food}`);

	it is very important that when you are including variables inside of something with the $ that you do not use quotes and u use the `` instead. as if you use quotes it will include the ${*var_name*} into the string instead of adding the VALUE to the string. 



There is also a Boolean data type. 

let name = "Jack"

let food = "pizza";

  

document.getElementById("who").textContent = `Hi ${name}`

document.getElementById("who").textContent = `Numa one food is da ${food}`


