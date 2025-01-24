
In order to create a Dropdown First create <div> section then create a button. We will then need another div section to  contain our dropdown menu.


In order to make your cursor into a pointer finger once you hover over it. 
    cursor: pointer; 



In order to make a dropdown menu in CSS that display only shows up when, hovered over and makes it grey and look good. Just make some Markup and make a Div  with the class dropdownmenu and then make  a button inside this div, then under the  button make another div in which you will store your content. Make the content Invisible until hovered over.

.dropdownmenu{

    display: inline-block;

}

.dropdownmenu button{

    background-color: grey;

    color:white;

    padding: 10px 15px;

    border:none;

    cursor: pointer;

}

  
  

.dropdownmenu a{

    display: block;

    color: white;

    text-decoration: none;

    padding: 10px 15px;

  

}

  
  
  

.dropdownmenu .content{

    display: none;

    background-color: grey;

    position: absolute;

    min-width: 100px;

    box-shadow: 2px 2px 5px hsl(0, 74%, 5%);

}

  
  

.dropdownmenu:hover .content{

    display:block;

}

.dropdownmenu:hover button{

    background-color: red;

}

  
  

.dropdownmenu a:hover{

    background-color: red;

}

this will also make the colors change when hovering over. 



it also makes the button an inline block so that it doesnt select it when your near the sides of it. 