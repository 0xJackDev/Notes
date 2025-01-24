

An Error Is an object that is created to represent a problem that occurs.
This occurs often with user input or establishing a connection


try { } = encloses code that might cause an error

catch { } = catch and handle any thrown errors from try {}.

finally { } = (optional) Always executes. Used mostly for clean ups like closing files, close connections and release resources 

try {

    console.log(x);

}

catch(error){

    console.log(error);

}

  

console.log('You have reached the end');



this prints the error ReferenceError: x is not defined


and then prints You have reached the end if i didn't have the catch error then the program would execute the 
console.log('You have reached the end'); but since we caught this error we can continue with our program. 
if we dont have a catch and an error it will produce this 

console.log(x);

console.log('You have reached the end');

Uncaught ReferenceError: x is not defined
    at script.js:4:13


try {

    console.log(x);

}

catch(error){

    console.log(error);

}

finally{

    console.log("this always execcutes ")

}

  

console.log('You have reached the end');



this will always execute the code inside of finally whether or not an error is produced and caught. after the try and catch runs. so we could always close connections and release resources whether theres an error or not.


const divident = window.prompt("enter a divedent");

  

const divisor = window.prompt("enter a divisor");

  
  

const result = divident / divisor;

console.log(result);



take this program. if someone tries to divide something by 0 it will display infinity so we could handle this with try and catch 


so if the user inputs 0 as the divisor then we want to cause an error so it doesnt output infinity 


  

try{

const divident = window.prompt("enter a divedent");

  

const divisor = window.prompt("enter a divisor");

  

    if(divisor == 0){

        throw new Error("You cant divide by 0")

    }

  
  

const result = divident / divisor;

console.log(result);

}

  

catch(error){

    console.log(error);

}


this will then log 
Error: You cant divide by 0


we can also make sure the input is a number by using

```
if(isNan(divident) || isNan(divisor)){{
	throw new Error("values must be a number");
}}
```