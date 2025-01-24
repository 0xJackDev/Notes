
A callback is a function that is passed as an argument to another function.

Used to handle asynchronous operations like reading a file, Network requests or interacting with databases.


These takes some time to complete and with javascript we don't necessarily wait for a piece of code to finish executing to continue on with our program we need a way to say Hey when you are done call this next.


  

function hello(callback){

    console.log('Hello');

    callback();

}

  

function goodbye(){

    console.log('goodbye');

}

  

hello(goodbye);


this will ONLY envoke the goodbye function after the hello() function has finished executing and executes callback(); Make sure you dont use () or it will call the function imediatly 



sum(displayresult, 1, 2);

  

function sum(callback,x, y){

    let result = x + y;

    callback(result);

}

  

function displayresult(result){

    console.log(result);

}



this program sets the sum functions callback to call back to the displayresult function once the sum function is done executing. 


sum(DisplayPage, 1, 2);

  

function sum(callback,x, y){

    let result = x + y;

    callback(result);

}

  

function displayresult(result){

    console.log(result);

}

  

function DisplayPage(result){

    document.getElementById('result').textContent = result;

}


this will instead set the callback function to Display page which will change the text content of the result id to equal the result. 