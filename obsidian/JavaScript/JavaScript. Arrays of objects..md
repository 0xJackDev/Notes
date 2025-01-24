
To create an array of objects just make sure you use {} inside of the array and seperate each object with commas for example

  

const fruits = [{name: 'apple', color:'red', calories:95},

               {name: 'orange', color:'orange', calories:45},

               {name: 'banana', color:'yeklow', calories:105},

               {name: 'coconut', color:'white', calories:159},

               {name: 'pinnaple', color:'yellow', calories:37},]



then in order to log the first name of the first object simply type the index value and then the property you want to access for example.

console.log(fruits[0].name);

which would index the first object and access the name and would log apple to the screen 

then we could push another object onto the end of the array like 

fruits.push({name: 'grapes', color:'purple', calories:'200'}); 


console.log(fruits[5].name);


this would return grapes (assuming you are using the code above at the top.)


this basically just works exactly like a normal array you can splice and split it and do everything. Just make sure to remember your working with objects not Individual variables 