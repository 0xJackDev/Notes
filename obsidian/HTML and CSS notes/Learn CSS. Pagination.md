

Pagination is the method in which a document is separated into pages, and numbers are given for each page. Using pagination we can move between pages either. This may be useful for limiting results. Say you dont want your screen to be cluttered with results you could use pages to display each result in a different page.


Usually Pagination is found at the bottom of a webpage 



To create this. First create a div element and then several hyperlinks inside of it for navigation and then center them and give them some CSS properties 

.Pagination a{

    color: grey;

    text-decoration: none;

    padding: 1.5em;

    display:inline-block;

}


<div class="Pagination">

<a href=""> <</a>

<a href="">1</a>

<a href="">2</a>

<a href="">3</a>

<a href="">4</a>

<a href="">5</a>

<a href="">></a>

     </div>


Now as you notice all of these hyperlinks have no href values we will change this. 



Lets give the page that we are currently on the hyperlink of that page a class of active. Then lets make that A different color so that users can tell which page they are on. In order to color the Pagination Class, Looking for all hyperlinks with a class of active use this CSS

.Pagination a.active{

    background-color: blue;

    font-weight: bold;

    border-radius: 5px;

}

Now in order to highlight all of the classes that are NOT active, and make them change when you hover over them BESIDES active class use this css. 
.Pagination a:hover:not(.active){

    background-color: grey;

    border-radius: 5px;

    color:black;

  

}

In order to have different "pages" you must have a separate HTML document for each "page" you would like, and set the href attribute to be that page in the hyperlink so when you click on it it brings you there. 