
This is the process of navigating through the structure of an HTML document using javascript.


HTML elements include but are not limited to

// .firstElementChild
// .lastElementChild
//  .nextElementSibling
// .previousElementSibling
// .parentElement
// .children


Lets discuss .firstElementChild,
Our unordered lists are elements, they each have their own children which is each <li> element inside of the ul tag

  

const fruits = document.getElementById('fruits')

  

console.log(fruits.firstElementChild);


for example 

<ul id="fruits">

    <li>Apple</li>

    <li> Orange</li>

    <li> Banana</li>

</ul>


this is the HTML code and above is the javascript code which would return 
<li>Apple</li>


  

```
const ulElements = document.querySelectorAll('ul');

  

ulElements.forEach(ulElements => {

    const firstchild = ulElements.firstElementChild;

    firstchild.style.backgroundColor ='yellow';

})

```

this would take the first element for every UL element and change the first list item background color to yellow  



.lastElementChild works like first element child but guess what! gets the last element instead!



Now lets talk about nextelement sibling


<ul id="fruits">

    <li id="apple">Apple</li>

    <li id="orange"> Orange</li>

    <li id="banana"> Banana</li>

</ul>

<ul id="vegtables">

    <li id="carrots">Carrots</li>

    <li id="onions"> Onions</li>

    <li id="potatoes"> Potatoes</li>

</ul>

<ul id="Deserts">

    <li id="cake">Cake</li>

    <li id="pie"> Pie</li>

    <li id="icecream"> Icecream</li>

</ul>


take this HTML code for example. If i selected cake and looked for the .nextElementSibling then i would select Pie, but if i Selected apple and looked for the next element i would get orange 


const element = document.getElementById("apple");

  

const nextSibling = element.nextElementSibling;

  

console.log(nextSibling);


for example this would return orange but if i changed apple to pie it would return  li#icecream 


.previousElementSibling works the exact same way as next element sibling except you guessed it! returns the previous element instead of the next


now lets talk about  .parentElement

This selects the parent element of whatever element you are using this method on, Take the same HTML code of the Lists above for example if selected apple and use the .parentElement method it would return ul#fruits

  

const element = document.getElementById("apple");

  

const parentElement = element.parentElement;

  

console.log(parentElement);


for example this would return fruits while if i changed apple to icecream it would return ul#Deserts





Now lets discuss the .children method.
This returns all of the children of a selected element for example if we selected the fruits unordered list it would return 

```
const element = document.getElementById("fruits");

  

const childrenelements = element.children;

  

console.log(childrenelements);
```

This would return 
HTMLCollection(3) [li#apple, li#orange, li#banana, apple: li#apple, orange: li#orange, banana: li#banana]

but if i changed fruits to Deserts instead it would list all the elements inside of Deserts 