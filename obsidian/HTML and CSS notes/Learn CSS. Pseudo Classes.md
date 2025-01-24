
Pseudo classes are keywords added to a selector. They modify the behavior. For example


button:active{

    background-color: aqua;

    left : 90%;


}


makes this so when i click on the button that makes it active




You can also do this with hyperlink say i want to make a hyperlink bigger when i hover over it.

a:hover{

    font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;

    font-size: 1.1em;

}




Lets say i make a list. And i want when i hover over one of the items in the list for that items background color to change do this. 
li:hover{

    background-color: yellow;

}

You could also make it so anything that is NOT being hovered other changes.

li:not(:hover){

    background-color: grey;

}


Lets say we make a div called greeting and put a p element in it and we only want that to Appear when we hover over it.

lets do this

#greeting p{

    background-color: aqua;

    display: none;

    padding:10px;

}

  
  

#greeting:hover p{

    display:block;

}



That will make its display none normally except when hovered over it becomes a normal block element. This Becomes really helpful for dropdown menus 