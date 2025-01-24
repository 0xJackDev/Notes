

This is explaining the position property in css.


There is 5 different possible things you can set your position attribute to


position: relative; 
position: fixed; 
position: absolute; 
position: sticky; 
position: static; 



with
position: relative; 
this positions an element relative to where it normally should be.

with our position property set to relative we can move this to the left, right, up or down.

In order to push this object down a certain value then i can set the top attribute with a certain value. 
    top:100px  ;
this will push down a object 100px relative to where it normally is.

another property is left so guess what if you set a left property with a value it will push that to the right how many pixels u tell it to. to move something all the way to the right you could type
left:100%

to move this element up set the top property to a negative number and to move it left set the left property negative 








With fixed position. the element is fixed to a position relative to the browser. 



for example if i have a box that is fixed to the top left corner and i have a long webpage, no matter how far i scroll down and what text goes into the box that box will stay over on the topleft

    right:0px;
    position: fixed;
    bottom:0px;

this would make an element stay fixed in the bottom right corner no matter what, good for ads.







Then we have absolute position. in this the position is relative to the nearest ancestor. 



#box1{

    width: 200px;

    height: 200px;

    background-color: hsl(199, 84%, 38%);

    position: relative;

    right:0px;

    bottom:0px;

  

}

  

*{

    box-sizing: border-box;

}

  

#box2{

    width: 50px;

    height: 50px;

    background-color: hsl(0, 84%, 38%);

    position: absolute;

    right:0px;

    bottom:0px;

  

}

for example this css right here. There is a div inside of a div. heres what i mean 
	<div id="box1">

    <div id="box2"></div>

</div>
	< div id="box1">

    <div id="box2"></div>

</div>



In this box2 is contained inside of box1, making the nearest ancestor to box2 box1. So when i set box2 with a position of absolute. the position is going to be relative to box1.  So if i set box1 to be in the bottom right corner then box2 will be inside of box1 in the bottom right while if box1 is in the top left so will box2. without changing anything with box2 only moving box1










Sticky element is positoned based on the current scroll position.  its similar to fixed except when it pops up it leaves room for the original element until you scroll down then it becomes fixed where it was. 





Static is the default position for an element 