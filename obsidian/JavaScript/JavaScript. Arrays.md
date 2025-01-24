

An array is a variable like structure that can hold more then one value. 

An normal variable like let fruit = 'apple'; Can only store one Value. But we can turn this into an array to store multiple by enclosing all values with a set of [] like this 

let fruits = ['apple', 'orange', 'banana'];


Make sure the separate all the different values with a , 


and if i console.log(fruits); javascript will print out every one of the elements inside of this array.

If you need to access an individual element in a array follows the variable name of the array you must add an index number enclosed in straight brackets. For example lets say I wanted to print the first Value "apple" to the console I would do this.  

  

let fruits = ['apple', 'orange', 'banana'];

  

console.log(fruits[0]);


if i changed this number to 1 it would print orange instead.


lets say I wanted to change banana to coconut i could just do 


let fruits = ['apple', 'orange', 'banana'];

  

fruits[2] = 'Coconut'

  

console.log(fruits[2]);


Which would log coconut. 



to add the element coconut to the end you could also change that 2 to a 3 which would add it in the third position but there is also a built in element to add to a array this is .push so to add coconut to the end

let fruits = ['apple', 'orange', 'banana'];

  

fruits.push('Coconut')

  

console.log(fruits[3]);


this would add coconut to the end and print coconut


there there is the .pop method which is gonna remove the last element so to get rid of banana at the end we could do


let fruits = ['apple', 'orange', 'banana'];

  

fruits.pop();

console.log(fruits);


which would only print apple and orange and remove banana



There is a way to also append to the begging of a array that is with the .unshift method


so to add mango to the begging we could do 

let fruits = ['apple', 'orange', 'banana'];

  

fruits.unshift('mango');

  
  

console.log(fruits[0]);


which would add mango to the beginning and print it 




then to remove an element from the beginging we can use the .shift method 

let fruits = ['apple', 'orange', 'banana'];

  

fruits.shift();

  
  

console.log(fruits[0]);


Which would remove apple and then print orange since it would be the first element 



to get the length of an array use the .length method 

let fruits = ['apple', 'orange', 'banana'];

  

let numofFruits = fruits.length;

  

console.log(numofFruits);


which would print 3 to the console


to search for a certain thing use the .indexOf method 


let fruits = ['apple', 'orange', 'banana'];

  

let index = fruits.indexOf('apple');

  

console.log(index);


this would print 0 as it is in the 0th or first place of the array if i looked for banana it would print 2. If you search for a element that doesnt exist though then it will ALWAYS return -1 this could be helpful in a if statement as you could search if a method returns -1 and if it does that means that that Value is NOT inside of the ARRAY ALREADY and you can do what you want with that.




let fruits = ['apple', 'orange', 'banana', 'coconut'];

  

for(let i = 0; i < fruits.length; i++){

    console.log(fruits[i])

}


this would print all of the elements in the array as long and the loop will keep going until i reaches 3, and since there is 4 elements in the array and both the loop and the first element starts at 0 it will print every element inside of the array on different line and loop a total of four times. 



if we needed to print an array backward we could reverse this 

let fruits = ['apple', 'orange', 'banana', 'coconut'];

  

for(let i = fruits.length; i >= 0; i--){

    console.log(fruits[i]);

}

except it would first print undefined as it is trying to index index 4 but index four doesnt actually EXIST since arrays start at 0 but since there is 4 elements in the array the i is originally set to four so to fix this change this to 

for(let i = fruits.length - 1; i >= 0; i--){

    console.log(fruits[i]);

}


there is a easier way to list each element in fruit with a for loop you could do 


let fruits = ['apple', 'orange', 'banana', 'coconut'];

  

for(let fruit of fruits){

    console.log(fruit);

}


which would print apple first then the rest of the arrays in sequential order 



to sort an array you can use the .sort method so fruit.sort();


let fruits = ['apple', 'orange', 'banana', 'coconut'];

  
  

fruits.sort();

for(let fruit of fruits){

    console.log(fruit);

}


this will sort the array in alphabetical order and display 
apple
 banana
 coconut
orange



to sort them in reverse just do 

fruits.sort().reverse();