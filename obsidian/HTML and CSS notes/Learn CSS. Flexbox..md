
within a container we can flex all of the elements. we do this by taking our container class and setting the display property to flex 

by default the flex-direction property is set to row 


to make it a row but in reverse we can do 
.container{

    display: flex;

    flex-direction: row-reverse;
    }

we could set flex-direction to be column as well or column-reverse.



then we have the justify-content property. Which sets the alignment o n the main axis. Think of the X axis or Horizontally. 


If you wanted to center these elements you can do

.container{

    display: flex;

    justify-content: center;

}


or to push them as right as the elements can go you could do
.container{

    display: flex;

    justify-content: flex-end;

}



by setting justify-content: space-between;  Itll spread the elements out as evenly as wide as the webpage can go 

.container{

    display: flex;

    justify-content:space-evenly;

}

this will space it evenly with spaces on the end as well. 





Then there is the cross axis think of this as up and down. in order to do this we must set the Height of the container element so that we can move the boxes up and down.

90vh means 90% of the vh of the webpage 

Now we can use the align-items properity to move up and down. 

The default is flex-start; which

.container{

    display: flex;

    justify-content:space-evenly;

    border:10px solid black;

    height: 90vh;

    align-items: flex-end;

}


flex-end will move it to the bottom of the View height. 

    align-items: center;
will center them.



Lets say we have 8 items and they are being squished we can set the flex-wrap property 

    flex-wrap: wrap;
will make the elements wrap around if there isnt enough space 


by default flex-wrap is nowrap 



there is also wrap-reverse. 




flex-wrap is used along another property called align-content. 


    align-content:flex-start; 


would make it so that when something is wrapped around there is no space in between and it just begins at the Leftmost spot under the other boxes. 



flex-end is the opposite where it wraps at the bottom



align-content:center makes it in the middle.


align-content:space-evenly; spaces it evenly.


and space-between puts the wrapped boxs all the way at the bottom.



ther is also the align-self property so that you can align an individual box.



This can be applied to any individual element. 



there is also the order property which works like lists in coding. for individual boxes


