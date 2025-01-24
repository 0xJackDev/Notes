

Destructuring allows us to extract values from arrays and objects and then assign them to variables in a coinvent way. 


// example 1. Swapping Variable values
[] = to perform array Destructuring

{} = to perform object Destructuring 


let a = 1;

let b = 2;

[a,b] = [b,a];

console.log(a);

console.log(b);

for example this performs Destructuring and reassigns value a to the value of b and then reassigns variable b to the value of a.  We can use Destructuring to swap two variables values.



// example 2. Swapping 2 elements in an array


const colors = ['red', 'greebn', 'blue', 'black', 'white'];

  

[colors[0], colors[4]] = [colors[4], colors[0]];

  

console.log(colors)


this would swap [colors[0], colors[4]] to replace it with the values of [colors[4], colors[0]] All this is basically doing is re assigning a variables inside the array to different indexes and moving them around this will print 
(5) ['white', 'greebn', 'blue', 'black', 'red']





//example 3. Assign array elements to variables


const colors = ['red', 'greebn', 'blue', 'black', 'white'];

  

const [firstColor, secondColor, thirdColor] = colors;

  

console.log(firstColor, secondColor, thirdColor);



this creates three parameters firstColor, secondColor, third color and assigns them each to the value of the array in their index. For example firstColor gets assigned to color[0] because its in the first index. while second color takes the value of colors[1];







// EXAMPLE 4. Extract Values from objects


const person1 = {

    firstname: 'spongebob',

    lastname: 'squarepants',

    age: 30,

    job: 'frycook',

}

  

const person2 = {

    firstname: 'patrick',

    lastname: 'star',

    age: 34,

}

  
  
  
  

const {firstname,lastname,age,job} = person1;

  

console.log(firstname);

for example this sets the variables firstname,lastname,age,job to be equal to the variables inside of the person1 object to global variables with Destructuring




//EXAMPLE 5. Destructuring in function parameters.

Meaning we can pass a Object to a function and destructure all the values when its passed in "making them Independent variables instead of object properties"



  

const person1 = {

    firstname: 'spongebob',

    lastname: 'squarepants',

    age: 30,

    job: 'frycook',

}

  

const person2 = {

    firstname: 'patrick',

    lastname: 'star',

    age: 34,

}

  

function displayPerson({firstname,lastname,age,job}){

    console.log(`Hi ${firstname} ${lastname} \n age: ${age} \n job:${job}`);

}

  

displayPerson(person1);



this would work to destructure this. The reason it works is because inside of the parameters we had the {} which automatically destructures any object that is passed to it And aligns it to the variables based on what index they are in. 


we could also set a default value incase one of the values inside passed for example person2 doesnt have a job so if we passed it through normally it would return undefined unless we change this too 

function displayPerson({firstname,lastname,age,job='Unemployed'}){

    console.log(`Hi ${firstname} ${lastname} \n age: ${age} \n job:${job}`);

}

  

displayPerson(person2);


which defaults to unemployed but if we passed person1 through it would overwrite the unemployed value and take frycook 