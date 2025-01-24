

a rest parameter is a parameter prefixed with three dots (...rest) this allows a function to work with a variable number of argurments by bundling them into a array. Similar to the spread operator but the opposite. 

Spread = expands an array into separate elements

rest = bundles separate elements into an array


const food1 = 'pizza';

const food2 = 'hamburger';

const food3 = 'hotdog';

const food4 = 'sushi';

  
  
  

function fridge(...foods){

    console.log(foods);

  

}

  

fridge(food1,food2,food3,food4);


this code above will print an array that says 
(4) ['pizza', 'hamburger', 'hotdog', 'sushi']

basically all this is doing is combining all the parameters given into one array 


if you wanted to separate them back into 4 different variables inside the function then you could use the spread operator onto the array foods. This is really really useful when you might not have the same amount of parameters going into a function each time. 


function sum(...numbers){

    let result = 0;

    for(let number of numbers){

        result += number;

    }return result;

}

  

const total = sum(1,2,3,4,5,6,7,7);

  

console.log(total);


you could put any amount of numbers inside of the sum function as arguments now this prints 35. 


function sum(...numbers){

    let result = 0;

    for(i = 0; i < numbers.length; i++){

        let number = numbers[i];

        result += number;

    }return result;

}

  

const total = sum(1,2,3,4,5,6,7,7);

  

console.log(total);


this would also do the same thing but with a for loop that actually makes sense to me I dont understand the Of bullshit 


function getAverage(...numbers){

    let result = 0;

    for(let i = 0; i < numbers.length; i++){

        let number = numbers[i]

        result += number;

  

    }return result / numbers.length

}

  

const total = getAverage(1,2,3,4,5,6,7,7);

  

console.log(total);


this is a function that will make the average which is 4.35 in this case


you can also use this to combine strings together 


function combineStrings(...words){

    return words.join(" ");

}

  

const total = combineStrings('mr', 'spongebob','-','thethird');

  

console.log(total);


this will combine all of the Strings together into one string with a space in between