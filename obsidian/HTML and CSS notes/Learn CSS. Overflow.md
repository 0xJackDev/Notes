
The overflow property sets the defined behavior when content doesn't fit in the parent element box, meaning it overflows.

There are five different states


overflow: visible;
overflow: hidden;
overflow: clip;
overflow: scroll;
overflow: auto;


If we have a border around something like text for example and we make the browser smaller. Alot of the times the text will overflow out of the box to handle this use the overflow property.


By default overflow is gonna be set to visible, basically we are stating if any elements will overflow then allow it to do so. This is why we see text overflow out of our borders


The second state is hidden, With hidden any content that will overflow out of our box will instead be hidden, where we can no longer see it.  However we can still interact with it for example if we copy and paste it. 




The third state is clip. This is very similar to hidden, there's no apparent change when overflow is set to clip it is used in tandem with the overflow-clip-margin property. With this we can set how far content overflows outside of the box. For example


#paragraph{

    border: 2px solid;

    height: 75px;

    overflow:clip;

    overflow-clip-margin: 13px;

  

}

this would allow the content to overflow by a maximum of 13 pixels 



The fourth overflow is scroll. in this it contains a scroll bar theres always a scroll bar even if the content doesnt need it.





The fifth and last overflow is auto this only gives a scroll bar when it is needed. 