

the .filter() method creates a new array by filtering out elements 


the .filter method only adds numbers to the array that when sent the function Return True!


let numbers = [1,2,3,4,5,6];

  

let evenNums = numbers.filter(iseven);

  

console.log(evenNums);

  

function iseven(element){

    if(element % 2 === 0){

        return true;

    }else{

        return false;

    }

}


this would return 2,4,6 to and log them to the console.


