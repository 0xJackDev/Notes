
index.html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

    <label id="countlabel">0</label><br>

    <div id="container">

    <button id="decreasebtn" class="button"> Decrease </button>

    <button id="resetbtn" class="button"> Reset </button>

    <button id="increasebtn" class="button"> Increase </button>

</div>

<script src="index.js"></script>

</body>

</html>


Javascript.

const decreasebtn = document.getElementById("decreasebtn");

const resetbtn = document.getElementById("resetbtn");

const increasebtn = document.getElementById("increasebtn");

const countLabel = document.getElementById("countlabel");

  

let count = 0;

  

increasebtn.onclick = function(){

    count++;

    countLabel.textContent = count;

}

  
  

resetbtn.onclick = function(){

    count = 0;

    countLabel.textContent = count;

}

  
  

decreasebtn.onclick = function(){

    count--;

    countLabel.textContent = count;

}


The thing i wanna keep in mind here is that we set four constants to equal the search for the element with id. This is so we dont have to search for the ID each time and we can just use the constant in order to work with that element. 