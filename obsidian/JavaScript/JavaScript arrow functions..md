
An arrow function is a concise way to write function expressions. This is good for simple functions you will only use once

(parameters) => *your code*;



  

const hello = () => console.log('hello');

  

hello();


this logs hello to the console. The reason () are there but empty is because we have no parameters but still need to follow the syntax of arrow functions 


in arrow functions if you want more then one segment of code then you must surround it in {} 

const sum = (num1,num2) => console.log(num1 + num2);

sum(1,2);

this would log 3 to the console.



you can also apply a foreach method

  

fruits.forEach(function log(fruit){

    console.log(fruit.calories);

})


this just logs each fruits calories. the value gets passed from the Foreach method to the Callback function named log which logs the fruits calories. 

way easier just to do 

fruits.forEach(fruit => console.log(fruit.calories));



This uses the map method to create a new array of all the fruits names. 
const FruitNames = fruits.map(fruit => fruit.name);

  

console.log(FruitNames);


