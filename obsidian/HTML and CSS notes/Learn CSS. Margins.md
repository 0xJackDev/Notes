


Margins are the space around a specific element.

If we create an element like a paragraph element for example and then right click on it in a webpage and inspect it we will see this box ![[Screenshot 2024-07-29 192725.png]]



The Text part of our paragraph is only contained within the blue part of this box, the margin part of this is gonna be blank space. The amount of space that an element takes up including all of this is its margin. Padding is between the element itself and any borders, and Margins are the area outside of any borders. Today we will work with Margins which are outside of any elements. Borders.



Naturally There is a few pixels of margin around our body. The elements of our paragraph aren't directly next to the border of our window  we can eliminate that like this.

First select the element which you wanna get rid of the margin.


p{

    margin: 0px;

}

By setting this. the Letters in the paragraph are going to by directly next to the edge of the web browser.

and if i was to set this margin higher there would be more area farther from the edge of the browser.


So all margin really is is the area outside of an element.


You can also  change individually margins on each side for example if you wanted the box to have no margin at the top but margin at the left use
\
#box1{

    margin-left: 100px;

}

which would only move your box to the right.

and its like that for any side so if you did margin-top it would only make space at the top.




I can also push one of these boxes all the way to the right side of my web page with 

#box1{

    margin-left:auto;

}

which would push my box all the way to the top right of the screen while 



If you would like an object to stay in the center of your web browser though you can just do 

#box1{

    margin:auto;

}

which centers the div to the middle. 
