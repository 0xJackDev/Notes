

The transformation property lets u rotate, scale, skew or translate an element 


    transform: translateX(50px);


If i was to set this box to have this css property it would move the box to the right 50 px 

    transform: translateY(50px);



Would move the box down 50 px 



Negative values will move the box left/Up. 

    transform: translateX(100%); 

would move it to the right as far as the box width is set 


    transform: translateY(100%); 
will move it as far down as the Height is set. 



you can do both of them at the same time with just translate(x, y) but you need two different value  with x being the first parameter and y being the second.


    transform: translate(50px, 50px);


would move the box down and to the right 50 pixels 








That's translations now we have rotation.  for this we set a number of degrees


    transform: rotate(45deg);

this would make the Box rotate to the right 45 degrees 

    transform: rotate(-45deg);



will make it rotate to the left




you can also rotateY

    transform: rotateY(80deg);


this will shrink the width idk its kinda weird.




there is also scale. you can scaleX or scaleY

    transform: scaleX(2)

This would make the X axis wider by 200% 


    transform: scaleY(1.5)
This scales the height makes it 150% taller  





Skew. Skews the Axis so you have skewY and skewX 




you can apply more then one transformation at a time. 

.container{

    transform: translateX(100px) rotate(45deg);

}


this moves the class container to the right 50px and rotate it 45 degrees 




you can also transform images.