


Introduction to height and width properties in css. 



Within our style sheet we can set an width and height for an element or an ID or class. 


By default height is auto, we can set the explicit height though for example 100 px. Width is the same way.


If you change the width to 50% for a block level elemt then the width will take up 50% of our viewport.


If you set a float value then you have to make sure that the two elements actually have room to float by each other, you gotta take things like border into account here. 2px of border can be the difference on whether something floats or not.



Padding can also do the same thing. Padding is simply the area around the element that isnt the border. So if you wanna move the border farther away from the element use more padding. If you wanna increase the white space after a border use the Margin.




When calculating the height or width we can disregade any padding or width but we have to add this property.
box-sizing: border-box;

This makes it so when we calculate the width and height, disregard any padding or borders. The box-sizing property changes this, it takes into consideration the padding and border so that the width and height would actually be 50% so you could float it. 



what some people like to do is to select all elements with * and apply.
*{

    box-sizing:border-box;

  

}



remember     
text-align:center; 
aligns our text to the center of the element.



We can also set max-width and min-width, or max-height, min-height. Which will make it so no matter whats inside of the element that the element will either be greater then this height or will not exceed this height or greater than this width and will not exceed with width.  




If we need our container in order to takeup the entire height of a webpage then we can create a container that takes up the body and sent that to we can set height to 
100vh;
vh standing for viewport height meaning our container takes up 100% of the viewport *browser* height.


.container{

    background-color: grey;

    height: 100vh;

}


