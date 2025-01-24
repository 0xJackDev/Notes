

In order to create a button first we will need a pair of < button > tags 




Heres a functional rounded green button that when clicks open google.com in a new tab 

<a href="https://google.com" target="_blank" >

<button style="background-color:green; border-radius: 5px;">

    Click me

</button>

</a>



This button in HTML works but it doesnt really have that much functionality. Thats where a language like JavaScript comes in.


When we click on this button we can have this button execute some function from a JavaScript file. Here is how we can create a very simple java script program.


After our begginging button tag we need to add the onclick attribute  that we can set to a javascript function we simply do 

<button onclick="function()">


Down in the HTML file lets create a paragraph element with an id attribute that id="test"



Heres how we can create a very simple java script program. First we are going to create a pair of script tags <script> </script> there is an opening and closing script tag 


<body>

  

    <h1> Hello </h1>

<hr>

<button onclick="dosomething()" style="background-color:green; border-radius: 5px;">

    Click me

</button>

<p id="test"> Hello</p>

  

<script>

    function dosomething(){

        document.getElementById("test").innerHTML = "Good Bye Button works!"

    }

</script>

  

</body>


This here above has a working document with a javascript function that when the button is clicked is called. The javascript function searches for a Element by the id with the name test that we set in the Paragraph element. It finds this in the Paragraph Element with the HTML text value of Hello inside. It then Makes the InnerHTML code of the document equal to "Good Bye button works "