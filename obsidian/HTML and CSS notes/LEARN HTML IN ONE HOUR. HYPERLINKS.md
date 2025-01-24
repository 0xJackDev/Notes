


Hyperlinks. 

We can apply hyperlinks to text, buttons, Images, and elements of that nature.

whatever you would like to be a hyperlink surrond by a pair of 

	<a> tags 


within the beginnging a tag there is a href attribute that you can set to a URL that you want the hyperlink to resolve to so for example if i want a hyperlink to google

	   <a href="https://google.com">

        Hyperlink</a>

This would make a Hyperlink that when clicked sends to google.


there is also a target attribute so that you can make the hyperlink open in a new tab add in the begging a tag target=_blank.


There is also a title attribute, this text appears when your curser hovers over the  hyperlink.



Say we wanted to make a hyperlink that points to another one of the HTML files on our website. We could do this by setting the href attribute equal to the relative file path of the html file we want to go to.

    <a href="page2.html" target="_blank" >

        Hyperlink</a>


Clicking this will take you to another html file. 


Lastly you can send a email to somebody within the href attribute. 

type href=mailto:emailaddr@gmail.com"

Then when we would click the hyperlink it would send a email.




<div class="Pagination">

<a href=""> <</a>

<a href="index.html" class="active">1</a>

<a href="page2.html">2</a>

<a href="page3.html">3</a>

<a href="page4.html">4</a>

<a href="page5.html">5</a>

<a href="">></a>



as you can see the > and <. >buttons do not have any functionality currently with javascript it would be easy to implement that if you are on page3 for example and hit the back button go to page2 and if you are on index.html and hit the forward button go to page2 But We dont know javascript so the easiest thing to do here is to hardcode the hyperlink attribute .



You also must make sure to take over the div for paginiation into every HTML file where you want this

    <div class="Pagination">

        <a href=""> <</a>

        <a href="index.html" class="active">1</a>

        <a href="page2.html">2</a>

        <a href="page3.html">3</a>

        <a href="page4.html">4</a>

        <a href="page5.html">5</a>

        <a href="">></a>
        


THENN in order to change which Element is highlighted, make sure to change the active class in each HTML document to represent which HTML document is active for example in page 1 its 

    <div class="Pagination">

        <a href=""> <</a>

        <a href="index.html" class="active">1</a>

        <a href="page2.html">2</a>

        <a href="page3.html">3</a>

        <a href="page4.html">4</a>

        <a href="page5.html">5</a>

        <a href="">></a>

but in page 2 it should be 
    <div class="Pagination">

        <a href=""> <</a>

        <a href="index.html">1</a>

        <a href="page2.html" class="active">2</a>

        <a href="page3.html">3</a>

        <a href="page4.html">4</a>

        <a href="page5.html">5</a>

        <a href="">></a>


and so on so fourth 



So what we could to add functionality to the < > thing is to individually in each HTML document make the < go back to the relative last file and the > to the next relative file for example page 2 would be like.
    <div class="Pagination">

        <a href="index.html"> <</a>

        <a href="index.html">1</a>

        <a href="page2.html" class="active">2</a>

        <a href="page3.html">3</a>

        <a href="page4.html">4</a>

        <a href="page5.html">5</a>

        <a href="page3.html">></a>
so on