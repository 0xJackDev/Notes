
In order to add a border around the element we simply use the. 
border-style: property. 

To make a solid border you can use 
border-style: solid; 

there's also a dashed border, dotted, double, groove, ridge, inset, outset, or none which removes a border if it has one.


you can change the border width with the guess what! border-width property. 


you can change the color with the border-color property.


you can round the corners with the border-radius property. with the higher the number of pixels the more rounded the borders will be.




there is also directional syntax, for example lets say you just wanted the bottom line of the border you can use 


border-bottom: 3px solid red;

There is three variables which you must set to use a directional border, The size in pixels, The Kind of border, And the color. for example 

.paragraph2{

    border-bottom:1px solid red;

}

and then border-right would be only to the right. border-top only the top, so on so fourth. 