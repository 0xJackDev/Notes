

the spread operator is represents by three dots "..." this allows an iterable such as an array or string to be expanded into separate elements. (unpacks the elements)




let numbers = [1,2,3,4,5];

let maximum = Math.max(numbers)

console.log(maximum);

if we do this it returns Not a Number or NaN. using the max method we cant place a array directly into the method but using the spread operator we can spread the array into different elements so precede the array with ... 


let numbers = [1,2,3,4,5];

let maximum = Math.max(...numbers)

console.log(maximum);

if we run this program it returns 5 which is true 


when you use the spread operator 


you can do this with strings too, and separate the string into different characters 


  

let username = 'bro code';

let letters = [...username];

console.log(letters);


this will print each char separately and make an array of characters. you could add a dash between each character like this

let username = 'bro code';

let letters = [...username].join('-');

console.log(letters);


let fruits = ['apple', 'orange', 'banana'];

let fruitcopy = [...fruits];

  

console.log(fruits);


this makes an EXACT copy of the fruits array and will print apple orange and banana 


we can also add two arrays togeth with the spread operator like this 


  

let fruits = ['apple', 'orange', 'banana'];

let vegatables = ['carrots', 'celery', 'potatoes'];

  

let foods = [...fruits, ...vegatables]

console.log(foods);



this combines the two arrays then prints it 



we even have the capabilites to append seperate elements without unpacking these. say we wanted to add eggs and milk to the array as well we can do 

  

let fruits = ['apple', 'orange', 'banana'];

let vegatables = ['carrots', 'celery', 'potatoes'];

  

let foods = [...fruits, ...vegatables, 'eggs', 'milk']

console.log(foods);
which will print 
(8) ['apple', 'orange', 'banana', 'carrots', 'celery', 'potatoes', 'eggs', 'milk']


Make sure you separate each element with a comma that you want to add into the array, if its not an array then you dont need to use the Spread operator. Or can turn a string into a array of chars





