
the Sort() method is used to sort elements of an array in place.

With this we sort elements as  strings in lexicographic order not alphabetical 

lexicographic = (alphabet + numbers + strings ) as strings 


  

const fruits = ['apple', 'orange', 'bananan', 'coconut','orange'];

  

fruits.sort();

  

console.log(fruits)


this would log  (5) ['apple', 'bananan', 'coconut', 'orange', 'orange'] in alphabetical order 


but i was to have numbers

const numbers = [1,2,3,4,10,22,44,2];

numbers.sort();

  

console.log(numbers)


this would return 

 [1, 10, 2, 2, 22, 3, 4, 44]

which is NOT in order of numbers, we are treating these numbers as strings that why we have 1 then 10 then 2 then 22 then 3 then 4.

so how do we fix this. We have to add a callback function inside of the .sort method to compare the numbers in index and make sure that it goes lowest to highest  


const numbers = [1,2,3,4,10,22,44,2];

numbers.sort((a, b) => a - b);

  

console.log(numbers)


this would log 

(8) [1, 2, 2, 3, 4, 10, 22, 44]


for reverse order so max to min you could do b - a. This will either return a postive or negative value and based on If it is Negative or not the function sort will know that the Number Being subtracted by is either larger or smaller then the number that it is subtracting and the .sort method will use this info to sort it properly. 


you could do this with objects as well just make sure to use the objects property identifier inside of the callback function so it knows where to find these properties. for example if you were sorting by age 

numbers.sort((a, b) => a.age - b.age);


for reverse order change b - a.


and it will reorder the Array to be sorted by age.


