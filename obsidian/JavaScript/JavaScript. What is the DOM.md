

The DOM stands for Document Object Model.

this is a javascript object that represents the page you see in the web browser and provides you with an API to interact with it. Web browser constructs the DOM when it loads an HTML document, and structures all the elements in a tree like representation. Javascript can access the DOM to dynamically change the content, structure and style of a webpage 

![[Pasted image 20240817120634.png]]



for example. This is why we type document.getelementbyid because document is an object and it contains all of our other objects.


if you were to console.log(document); it would display your entire HTML document 



for example

document.body.style.backgroundColor = 'black';

this would turn the entire document body background to be black. Making the background of your entire webpage black 