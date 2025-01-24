

To use a animation we must first create an animation using a keyframe rule that can be done like this 

@keyframes slideleft{

}


With slideleft being the Unique Identifer name. of the animation.


Inside of the keyframes you  have a few different options 

@keyframes slideleft{

    from{transform: translateX(400px);}

}

This makes an animation that transforms whatever you put it in to make a box start at the right and move to the left 400px. In order to use this you must select an element and provide two Attributes.

    animation-name:slideleft;

    animation-duration: 2s;


Animation name is the name of the animation and animation duration is how long the animation takes to fully happen.



Since the animation used the from selector it start at 400px and moved to the left but if we wanted to make it start at the begining and move to the right we can do 

  

@keyframes slideright{

    to{transform: translateX(400px);}

}



as you can see we changed the keyword from to to. 



bascially we can use the tranform property for animations.


  

@keyframes Rotate180{

    50%{transform: rotatez(180deg);}

}

will flip the element upside down then flip back right up.


@keyframes rotate360{

    25%{transform: rotatez(360deg);}

}


if i was to make it 25% it the animation would be ALOT faster it would say i have a 2 second animation duration it would complete it in  .5 seconds or 25% of 2. 



@keyframes scaleup{

    100%{transform: scale(2, 2);}

}

this would increase the width and height by 200% then shrink it back down 



@keyframes scaledown{

    100%{transform: scale(.5, .5);}

}


will make Width and height shrink to 50% of what it was.



the first keyword in animation unless you are moving something on the y or X axis is always going to be a percentage. 


  

@keyframes fade{

    100%{opacity: 0;}

}


This makes a element fade away and then come back, 


@keyframes changecolor{

    50%{color:red;}

}


this changes the color. Basically you get the point you can add any property into an animation pretty easily 



@keyframes Americaa{

    0%{background-color:red;}

    30%{background-color:white;}

    80%{background-color:blue;}

  

}


this would change the colors to red white and blue first red, second white, third blue 


  

@keyframes slideleft{

    80%{background-color:red;}

    30%{background-color:white;}

    0%{background-color:blue;}

  

}


If i changed it to this it would be blue first, then White then red. This is because of the percentage values. These mark at where the animations begins and ends in relation to the animation duration so in this the color red is changed when it has reached 80% of the animation length. 


THE PERCENTAGE VALUE MARKS WHEN THAT Percentage Completes at. 


@keyframes slideleft{

    0%{background-color:red;}

    30%{background-color:white;}

    80%{background-color:blue;}

  

}

  

#box:hover{

    animation-name:slideleft;

    animation-duration: 5s;

}



This would make it so when i hover over the box for 5 seconds it turns Red White then Blue. 




To have an animation occur more then once we can set the 


animation-iteration-count: 

if you set this value to 2 for example it will play the animation twice. If you want it to be infinite set it to infinite




we can also change the animation-direction property.

say its moving left to right and instead of changed the keyframe we to make it move right to left we could just do animation-direction:reverse;



to pause the animation we can set


animation-play-state: paused;

to make it run.
animation-play-state: running;



theres also a animation-timing-function: 