
this is a function that allows you to schedule the execution of a function after an amount of time in milliseconds. Times are approximate and based on the workload of the javascript runtime env 

this is the syntax
setTimeout(*callback*, *delay*)


  

function sayHello(){

    window.alert('hello');

}

  

setTimeout(sayHello,3000);


this will display an alert that says hello after 3 seconds