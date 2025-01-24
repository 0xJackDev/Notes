

This is all about how to create text shadows and box shadows


In order to set a text shadow you must select the element with the text and use the 
text-shadow attribute. which takes two variables. A horizontal offset and a vertical offset. So if we do 
text-shadow: 1px 1px; 

we have an offset to the right of one and down by one.


text-shadow: *Right/left*, *Up/down*;

For example 


h1{

    text-shadow: 10px 10px;

}

you can also add a third number for a pixel blur. you can also pick a color in this for example. 

h1{

    text-shadow: 10px 10px 19px red;

}

has a blurry red shadow. 



You can also add more then one shadow in order to do this just seperate them with a comma inside of the same text-shadow line and it will work for example


h1{

    text-shadow: 10px 10px 19px red, 20px 30px 19px blue;

}

gives a red and blue blur, 




Now lets work with box shadows. 

First to create a box create a <div> and then we can add properties to this emptey div in css so lets give it some width, and height and a color.  and then apply a shadow to it.


For other elements besides test we have box-shadow. 
This box-shadow takes the same variables as the text-shadow function with the horizontal and vertical offsets, then blur and color.

#title{

    width: 100px;

    height: 100px;

    background-color: grey;

    box-shadow: 5px 5px 5px red, -5px -5px 5px blue;

}

This adds css properties to make a grey box with a cool little border of blue and red shadows out of an emptey div. 
