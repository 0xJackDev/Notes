
a closure is a function defined inside of another function. 

the inner function has access to teh variables and the scope of the outer function.

Allows for private variables and  state maintenance.

Used frequently in JS frameworks like React, Vue or angular.


for example


function outer(){

  

    function inner(){

    }

}


the inner function has access to all variables inside of the Outer function. 

function outer(){

    let message = 'Hello';

    function inner()

    {

        console.log(message);

  

    }

  

    inner();

}

  

outer();



when we call the outer function it runs then at the end it calls the inner function which displays the message Hello world using the variable declared in the outer function. 
Though we cant just call the function inner(); directly it will say. Inner is not defined since it is the local scope of the outer function. 



a closure can also maintain the state of a program.



function increment(){

    let count = 0;

    count++;

    console.log(`Count increased to ${count}`);

}

  

increment();

increment();

take the program for example above. It actually prints 
Count increased to 1
Count increased to 1

instead of incrementing the count to 1. This is because we actually redeclare the function every single time that we call it and "reset" the function entirely. 


  

function createCounter(){

    let count = 0;

    function increment(){

        count++;

        console.log(`Count increased to ${count}`);

}

    return {increment};

}

  

const counter = createCounter();

  

counter.increment();

counter.increment();

counter.increment();


this creates an object called counter and then we return the increment function each time that we call this object. Resulting in 
Count increased to 1
 Count increased to 2
Count increased to 3




