
HTML elements have a default display value, they are either block-level or inline. 




An Block-level element is an element that starts on a new line and takes up the full width available 
- (h1, div, p, form, header, footer)






An inline element does not start on a new line and width is limited to what is needed
- (span, a, img).



By using the display property we can specify if and how an element is displayed, we can set an element to be a block-level, inline element. inline-block or not display it at all. 





Div is a block level element, meaning it takes up the whole width. While span is an in line element you can tell the difference here


<div style="background-color: red;">eere</div>

<span style="background-color: blue;"> span</span>


With the div, you can set a width and a height, but for an inline element the width and height wouldn't apply as the area that the element takes up is only around the text, so width and height properties in css dont work for example.

<div style="background-color: red; width: 100px; height:100px;">eere</div>

<span style="background-color: blue;  width: 100px; height:100px;"> span</span>


as you can see i applied the same inline css properties to both but the inline element "span" doesnt do anything with it and stays the same size. by utilizing the display property we can change the behavior of these elements. keep in mind when u click on the code the only reason im using inline css is so it shows up on obsidian, use external css for anything in production. For example if i set my span element to block level display.

<div style="background-color: red; width: 100px; height:100px;">eere</div>

<span style="background-color: blue;  width: 100px; height:100px; display: block;"> span</span>



There is also inline-block display. it is much like inline except we can apply a width and a height. but it also doesnt take up the whole window. 




There is also display:none; which will erase the element like it never existed



there is also the visibility property. 

if you set
visibility: hidden; then the element will be hidden but take up space as if it was there. while display:none deletes it completly. 