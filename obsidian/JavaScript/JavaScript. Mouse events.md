
an eventListener listens for specific events to create interactive web pages. There are Click events, Mouseover Events for when we hover over something, and Mouseout events for when we stop hovering over something

to add an event listener use the .addEventListener method with the syntax being

.addEventListener(*event*, *callback function*)

for example

  

const mybox = document.getElementById('mybox');

  

mybox.addEventListener("click", changeColor)

  

function changeColor(event){

    console.log(event);

    event.target.style.backgroundColor = 'black';

  

}


this changes the element called mybox to upon being clicked changes the background color of the element. You may notice we add to the .target method after the event, that is so that we know what we are targeting. Also you may notice we dont pass through the Event Argument to the function Changecolor even though it takes that parameter. That is because it is auto included in the addEventListener Method. 


const mybox = document.getElementById('mybox');

  

mybox.addEventListener("mouseover", changeColor1)

mybox.addEventListener("mouseout", changeColor2)

  

function changeColor1(event){

    console.log(event);

    event.target.style.backgroundColor = 'white';

  

}

  
  

function changeColor2(event){

    console.log(event);

    event.target.style.backgroundColor = 'blue';

  

}

This orignally is a green box, but when you hover over it it will turn white, 
