

a function expression is a way to define functions as a value or a variable.

a function declaration is a way to define a reusable block of code that performs a specific task.
a function declaration would be 
function max(accumlator, element){

    return Math.max(accumlator, element);
}



with a function expression we can assign a function to a variable or pass it as a value to another function for example.

const hello = function(){

    console.log('hello');

}
hello();

for example this create a function and then assigns it to the variable hello. To evoke this function we called the variable hello(); with a set of parenthesis 

we can also pass a function as a value. 


const hello = function(){

    console.log('hello');

}

  

setTimeout(hello, 3000);

this code here passes the hello function as a parameter to the settimeout function, the 3000 tells the browser to wait 3000miliseconds to envoke the hello function 



Function expressions are a way to define functions as values or variables.



