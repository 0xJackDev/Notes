

Element selectors are methods that allow you to target and manipulate HTML elements this allows you to select one or more HTML elements from the DOM 


	1. document.getElementByID() Selects a element or NULL.


	2.document.getElementsClassName() 
		Selects an class of elements 



	3. document.getElementsByTagName()
		selects all elements with a certain tag for example document.getElementsByTagName('h1). Would select all h1 elements 

One important thing to note about HTML collections which is 2. and 3. is that they are not arrays, for example you could not apply the forEach() method to an HTML collection. Instead you would have to turn it into an array first then you could access it.

for example

const fruits = document.getElementsByClassName('fruits');

Array.from(fruits);

will turn it into an array and now u can interact with it as such. 


Although these HTML collections are not arrays. You can still index the indivudal elements in them like an array for example 

const fruits = document.getElementsByClassName('fruits'

fruits[0]; Will return the first fruit element in the fruits class, but if you wanna apply array specific methods you must convert it to an array




	4.document.querySelector()
		This will return the first matching element. Or null if it doesnt find any matches for example

  

```
const element = document.querySelector('.fruits')

console.log(element);
```



this will log 
h1 id="test" class="fruits"> First fruit</h1>


as it is the first instance of the Fruit class. This searches sequentially from top to bottom so which ever fruits class element is on the top first will be returned.

you can also select tags or ids to search for not just classes. 



	5.document.querySelectorAll()
		This returns a NODELIST, which is similar to a HTML collection but it has built in methods similar to an array. However NODELISTS are static while HTML collections are live. Since NODELISTS are static they do not update automatically in the DOM like HTML collections do. 

  

const elements = document.querySelectorAll('.fruits')

  

console.log(elements);


this will return 


1. NodeList(3) [h1#test.fruits, h1#test.fruits, h1#test.fruits]

1. 0: h1#test.fruits
2. 1: h1#test.fruits
3. 2: h1#test.fruits
4. length: 3
5. [[Prototype]]: NodeList

the #test is the ID of the elements they all have the same ID since i put it like that in my HTML document. But that is bad practice im just eepy :3


Nodelists have a built in foreach method so you can just use 

const elements = document.querySelectorAll('.fruits')

  
  

elements.forEach(elements => {

    elements.style.backgroundColor = 'yellow';

})


which will turn all the objects in the .fruits class background color yellow 
