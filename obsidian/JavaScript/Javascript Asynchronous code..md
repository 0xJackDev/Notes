


synchronous code = executes line by line consecutively in a sequential manner. This code waits for an operation to be complete to move to the next. 



Asynchronous code allows multiple operations to be performed concurrently without  waiting. Doesnt block the execution flow and allows the program to continue. (I/O operations, Network requests, Fetching data) Handles with callbacks, Promises and Async/Await.


  

setTimeout(() => console.log('Task 1', 3000));

  

console.log('task 2');

console.log('task 3');

console.log('task 4');

console.log('task 5');


for example this would execute 
task 2
 task 3
task 4
 task 5
 Task 1 



This is because setTimeout is one of many asynchronous operations 

