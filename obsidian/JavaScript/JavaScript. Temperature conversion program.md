
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

<h2>

<label for="inputform" style="font-size: 2em;"> Tempature conversion: </label> <br>

<input id="inputform" type="number" value="0"> <br>

  

<input type="radio" id="toFaren" name="unit">

<label for="toFaren"> Celsius ➡️ Farenheit </label> </label>

<br>

<input type="radio" id="toCels" name="unit">

<label for="toCels"> Farenheit ➡️ Celsius </label> </label>

<br>

<button id="submitbtn" onclick="convert()">Submit</button>

<p id="result"></p>

</h2>

  

<script src="index.js"></script>

</body>

</html>


const submitbtn = document.getElementById("submitbtn");

const result = document.getElementById("result");

const toCels = document.getElementById("toCels");

const toFaren = document.getElementById("toFaren");

const inputform = document.getElementById("inputform");

  
  

let temp;

  

function convert(x){

    if(toFaren.checked){

        temp = Number(inputform.value);

        result.textContent = temp * 9 / 5 + 32 + 'F';

  

    }else if(toCels.checked){

        temp = Number(inputform.value);

        result.textContent = (temp - 32) * (5/9) + 'C';

  

    }else{

        result.textContent = 'Please Select a Unit.'

    }

}