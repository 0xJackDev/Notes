

first we need to store our random number in a variable to create a random number we can use the random method inside of math so Math.random();

this will generate a random number between 0 and 1

for example .79034732742374732


Lets say we would like to roll a 6 sided dice we would need a RNG from 1-6. The first step is to multiply math.random() by 6. and we also dont want a decimal so we do

```
let randomnum = Math.random() * 6;

let result = Math.trunc(randomnum);

console.log(result);


Our random number will be between 0 and 5. but we need 1-6 so we can increase the minimum by adding +1. or whatever u want the min to be 

let randomnum = (Math.random() * 6) + 1;


for a random number between 1 and 100 you can do 

let randomnum = (Math.random() * 100) + 1;


lets say you want a range of numbers from 50-100

let randomnum = (Math.random() * (100 - 50)) + 50;

we have to subtract 50 since we are adding on 50 and we dont want it to be above 100 max. and its gonna add 50 to every number we generate so even if we generate a 0 it will * 50 then add 50 to it.
```