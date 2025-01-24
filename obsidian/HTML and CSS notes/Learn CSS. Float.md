

The float property allows other elements to flow around it. This is particular useful for images and block level sections like div sections. 

If i have a div element say above a paragraph its gonna take up the entire width of the space in my web browser, and any elements after will just be pushed underneath. Its possible utilizing float property to have this text wrap around this block level element. In order to do this we must set a float property inside of the css of the image/block.


Without float.
No css.
![[Screenshot 2024-07-29 194740.png]]

With float: left;
#img1{

    float: left;

}

![[Screenshot 2024-07-29 194827.png]]

with float: right;

#img1{

    float: right;

}![[Screenshot 2024-07-29 194840.png]]



If the float is to close to the image you can make sure to add margin. 


If we have images that are floated and we decide to add a border to out body the images are going to be misplaced and out of the border alot of the times to fix this just do 

body{

    border:solid;

    display:flow-root;

}

and anything within the bodies including floating things will stay within container and not overflow.