
the forEach method is used to iterate over the elements of an array and apply a specified function (callback) to each element.


let numbers = [1,2,3,4,5];

  

numbers.forEach(display);

  

function display(element){

    console.log(element);

}

this would apply the Display method for each number and then log each number to the console separately 

let evennumbers = [];

  

let numbers = [1,2,3,4,5,6];

  

numbers.forEach(display);

  
  

function display(element){

    if(element % 2 == 0){

        evennumbers.push(element);

    }

}

  

console.log(evennumbers)

for example this would log 2,4,6 because they are even.


the element argument is provided for us by the for each method by default the foreach() method gives us a element, index and array values to pass to the callback function so if i wanted to log each one for which index is in the  array.


let evennumbers = [];

  

let numbers = [1,2,3,4,5,6];

  

numbers.forEach(display);

  
  

function display(element,index,array){

    console.log(index);

}


this would log 0,1,2,3,4,5 to the console. Since the element index and array are provided by the foreach function The first Parameter is always gonna be the individual element the second is always gonna be the index of that element and then the third will be the full array 