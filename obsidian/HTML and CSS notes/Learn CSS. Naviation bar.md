

We are going to use a <nav> element also known as a navigation element. These are typically used for a set of naviagation links 


Here is the html for the navbar
<nav class="navbar">

    <ul>

        <li><a href="">home</a> </li>

        <li><a href="">about</a> </li>

        <li><a href="">products</a> </li>

        <li><a href="">contact</a> </li>

  
  

    </ul>

Under this we will have a <main> section with our main content.


and replace the HREF with the html file you want to bring it to 

In our CSS

body{

    margin: 0px;

}

  
  

main{

    margin: 1.2em;

}

  

h1{

    text-align: center;

}

  
  

.navbar ul{

    list-style-type: none;

    background-color: grey;

    padding: 0px;

    margin: 0px;

    overflow: hidden;

}

  
  

.navbar a{

    color: white;

    text-decoration: none;

    padding: 15px;

    display:block;

    text-align: center;

}

  

.navbar a:hover{

    background-color: hsl(0, 0%, 19%);

}

  
  

.navbar li{

    float: left;

}




First we are gonna make it so that the Nav bar has no margin but the main body does. Then we are gonna align the text and then in the .navbar ul section we make it so any content that overflows on the float is hidden. And then we center all the hyperlinks. We then make the navbar List float so that content can flow around it while it sticks to the left. 