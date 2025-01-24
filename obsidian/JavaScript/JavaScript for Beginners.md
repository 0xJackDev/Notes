

First we need to link the JavaScript file to the HTML file we can do that by adding a pair of <script> </script> tags in the body part of the html doc for example.

You do want your Script element at the bottom of your HTML file so that incase there is an error all of your HTML elements render first before running any javascript code.
    <script src="index.js"></script>




	In order to ouput some text to the console you can use console.log(); function. For strings you can use "" '' and  ` ` 




There is nothing gonna appear on the webpage but if you go to Dev tools and then console it will print something in the console.



In our webpage to create an alert box we can type 


window.alert("This is a alert");


which will pop something up at the top of your HTML document with an alert 


you can comment stuff out in JavaScript same as C++ with // 


Comments in JavaScript and C++ are the same.


In order to interact with an HTML element in JavaScript you must set an ID/Class for these elements  for example lets say i have an h1 element with an id of who to interact with that lets type. 



document.getElementById("who").textContent = 'Hello333';


As you can see the document.getElementbyId() function selects a specific element by the id in this case who and then we use copy initalization to set the value to this element to Hello333. Changes the Html Markup to Hello333


the .textContent after makes sure you are selecting the text content of the element. 