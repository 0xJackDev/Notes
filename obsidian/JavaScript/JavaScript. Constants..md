

A const short for constant is a variable that cant be changed once you assign them


lets make a program that calculates the area of a circle from the radius 


let pi = 3.14159;

let radius;

let circumference;

  

radius = window.prompt("enter radius of circle : ")

radius = Number(radius);

circumference = 2 * pi * radius;

console.log(circumference);



Why would you want to use a const in this? Someone may accidently or maliciously change the value of a variable so that the program doesn't behave as intended. Lets say somehow somewhere in the program pi got reassigned well then our whole program would break. To make it so this cant happen we must change our variable to a constant to do this with pi do 
const PI = 3.14159;

It is good practice that if you have a const make the Variable name all uppercase. only Do this with Simple data type (Numbers and Booleans) not 
with Strings you dont need to uppercase them.

And if we try to reassign PI to a different value we get an untype caught error. 


  

const pi = 3.14159;

  

let radius;

let circumference;

  
  

document.getElementById("button").onclick = function(){

    radius = document.getElementById("textbox").value;

    radius = Number(radius);

    circumference = 2 * pi * radius;

    document.getElementById("h3").textContent = `The Circufrence based on radius is: ${circumference}`;

}



This is the javascript code that will take an input form  radius, then based on radius calculate the circumfrence and display it on the webpage. 