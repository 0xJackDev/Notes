
Lets break down Appending and adding elements to the DOM in three steps

Step 1 Create the element

Step 2 Add attributes and properties to the element

Step 3 Append element to DOM 


Lets walk through the steps and how we can do them

First to create a new element we can use the document.createElement(*'typeofelement*) method for example 
for example
const newH1 = document.createElement('h1');

this creates a new h1 element and refences it to newH1 constant





Now lets do step 2
newH1.textContent = 'I like pizza';
This adds text content to the new H1 element. But it still doesnt appear till we do step 3


Step 3. Append to DOM
document.body.append(newH1);
Append adds to the END of the element which you are adding to in this case the body element, so at the end of our Body element which is everything we will see we like Pizza. But we want this to be a Header in the begging well instead of append we can use prepend 

document.body.prepend(newH1);

Which adds to the top. 




In total. 

// step 1: create element

const newH1 = document.createElement('h1');

  

// step 2: add value to element

newH1.textContent = 'I like pizza';
newH1.id = 'myH1';
  
  

// step 3: Append element to DOM

document.body.prepend(newH1);



This also adds a ID to our element in step 2 as you can see 


we could also add newH1.style.color to change the text color or we could do any CSS elements after the .style method to change anything 
for example 

newH1.style.textAlign = 'center';

will center the text 



but in step 3 you see that we append the element to the body. What if instead we wanted to append/prepend it to box1 so it would be in box 1 well we could do 

document.getElementById('box1').append(newH1);


Which would first search for this element then use method chaining to add it append newH1 to it. 


if we wanna insert something before we can use the .insertBefore method 





if you ever need to remove an HTML element you can do this

document.body.removeChild(newH1)
this is assuming it lies as a child of the body element but what if it was a child of the box1 element then we could do this 

document.getElementById('box1').removeChild(newH1);

This would remove it.

as you can see if we arent searching for a body first we need to find that element by ID 



Now lets say we have a order list and we want to create and add a new item to it we could do this. 
```

// step 1: create element

const newListItem = document.createElement("li");

  

// step 2

newListItem.textContent = 'coconut';

  

// step 3

document.getElementById('fruits').append(newListItem);


```



You can add this with DOM navigation methods to add stuff before elements or after and stuff. If the list items not have IDs then we could use query selector for example and select all fruits and then add our element to the index we want it to be added at.