
CSS stands for cascading style sheets. We can apply CSS properties to decorate our HTML markup file. Theres three different ways in which we can apply CSS. 



Inline,  Internal, and External.


We will start with inline.


suppose we have a h1 header tag with a title of this is my website.  In order to apply css values to one of our elements. we  have to select the opening tag and add the style= attribute with the CSS properties you want.

<body style="background-color:black ; color: white;">

this is an example of inline CSS, within the opening tag you can change the style attribute. 





Another method of applying CSS is internal. as in an internal style sheet. 


	To apply an internal CSS style sheet within the head of our document we need to add a pair of <style> </style> tags. Whatever elements you would to apply css to you would add that within the style tags. For example if you wanted to apply properties to the body. You would type

For example 

    <style>

        body{

            background-color: black;

            color:white
</style>

        }

Make sure this is within the head portion of your HTML file and not your body. 

then to affect for example the paragraphs you could do 

        p{

            width: 500px;

        }







Now lets create an external style sheet.



External style sheets are the most popular method because we can make a style sheet that is reusable . In order to create this we need to create a new .css file inside of the same folder with out index.html file .


Create a File called style.css

we then need to link this style.css file and the index.html file together. 

We can do that within the head tag of the html document by using a <link>  tag  for example. 

<link rel="stylesheet" href="style.css">

This is what a valid link tag looks like, its telling the browser that the file we are looking for is a stylesheet/css file and that its name is style.css.

Using this external style sheet document we can select specific elements from our HTML file and apply css properties, this works pretty much the same format as internal, except we dont need a style tag. so if we wanted to select the body then make the text white and the background black we would do

body{

    background-color: black;

    color:white;

}

all we have to make sure is to include the css file in the head of the html document and itll work.


If you need to apply CSS properties to one specific line, for example if we have four paragraph elements but only want the first one to be affect we can create an ID within this elements opening tag. 

for example 

<p id="p1">Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime minus ipsum repellat molestiae ipsa culpa dolores ratione impedit praesentium quo eius non dolor animi deleniti, ullam nostrum aspernatur facilis illum!</p>

<p id="p2">Lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio minus provident ipsam voluptate consequatur aperiam! Dolores tenetur dolorum voluptate suscipit doloremque ad error libero ipsam vero adipisci, rerum magnam atque!</p>

<p id="p3"> Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum, in. Ipsam totam eveniet architecto fugiat, ut sequi dolor corrupti accusamus id. Similique, incidunt? Eligendi minima fugit pariatur provident cum ullam!</p>


To select an element by ID you will use a hashtag and then the id so to interact with the p1 element  do


#p1{

color:red;

}

would make the first paragraph red 




#p1{

color:red;

}

  

#p2{

    color:orange;

}

  

#p3{

    color:yellow;

}


Would change all the colors of the paragraphs to different colors.






You can also apply CSS properties as a class/group.

you can add these elements to a group by in the opening tags adding the class= attribute for example to make all three of those paragraphs in the same class you can 

<p id="p1" class="paragraph">Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime minus ipsum repellat molestiae ipsa culpa dolores ratione impedit praesentium quo eius non dolor animi deleniti, ullam nostrum aspernatur facilis illum!</p>

<p id="p2" class="paragraph">Lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio minus provident ipsam voluptate consequatur aperiam! Dolores tenetur dolorum voluptate suscipit doloremque ad error libero ipsam vero adipisci, rerum magnam atque!</p>

<p id="p3" class="paragraph2"> Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum, in. Ipsam totam eveniet architecto fugiat, ut sequi dolor corrupti accusamus id. Similique, incidunt? Eligendi minima fugit pariatur provident cum ullam!</p>



This example i made two groups in one group theres two paragraphs and in one class it is alone. 


In order to add css propterties to a class you must first start with a . for example

.


.paragraph{

    color:white;

}

  

.paragraph2{

    color:red;

}



Changes the css properties for both the groups 