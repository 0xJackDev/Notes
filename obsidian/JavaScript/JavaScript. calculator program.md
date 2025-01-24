
HTML
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

    <div id="calculator">

        <input id="display" readonly>

        <div id="keys">

            <button onclick="appendToDisplay('+')" class="operator">+</button>

            <button onclick="appendToDisplay('7')">7</button>

            <button onclick="appendToDisplay('8')">8</button>

            <button onclick="appendToDisplay('9')">9</button>

            <button onclick="appendToDisplay('-')" class="operator">-</button>

            <button onclick="appendToDisplay('4')">4</button>

            <button onclick="appendToDisplay('5')">5</button>

            <button onclick="appendToDisplay('6')">6</button>

            <button onclick="appendToDisplay('*')" class="operator">*</button>

            <button onclick="appendToDisplay('1')">1</button>

            <button onclick="appendToDisplay('2')">2</button>

            <button onclick="appendToDisplay('3')">3</button>

            <button onclick="appendToDisplay('/')" class="operator">/</button>

            <button onclick="appendToDisplay('0')">0</button>

            <button onclick="appendToDisplay('.')">.</button>

            <button onclick="calculate()">=</button>

            <button onclick="clearDisplay()" class="operator">C</button>

  

        </div>

  
  
  
  

    </div>

  

    <script src="script.js"></script>

</body>

</html>


Javascript

  
  
  

const display = document.getElementById('display');

  
  
  

function appendToDisplay(input){

    display.value += input;

}

  
  

function calculate(){

    try{

    display.value = eval(display.value);

    }

    catch(error){

        display.value = "Error"

    }

}

  
  

function clearDisplay(){

    display.value = "";

  

}



CSS:

button{

    width: 100px;

    height: 100px;

    border-radius: 50px;

    border: none;

    background-color: black;

    color:white;

    font-size: 3rem;

    font-weight: bold;

    cursor: pointer;

    text-align: center;

}

  

#keys{

    display:grid;

    grid-template-columns: repeat(4,1fr);

    gap:10px;

    padding: 25px;

}

  

#calculator{

    font-family: Arial, Helvetica, sans-serif;

    background-color: hsla(0, 0%, 8%, 0.966);

    border-radius: 15px;

    overflow: hidden;

    max-width: 500px;

  

}

  
  

#display{

     width: 100%;

     padding: 20px;

     font-size: 5rem;

     text-align: left;

     border: none;

     background-color: hsla(0, 0%, 8%, 0.548);

     color:white;

    }

  

body{

    margin:0;

    display: flex;

    justify-content: center;  /* aligns items vertically */

    align-items: center; /* aligns items horinzontally */

    height: 100vh;

}

  

button:hover{

    background-color: hsla(0, 0%, 0%, 0.171);

}

  
  

button:active{

    background-color: hsla(0, 0%, 21%, 0.336);

}

  

.operator{

    background-color: hsla(35, 100%, 50%, 0.719);

}

  

.operator:hover{

    background-color: hsla(35, 100%, 65%, 0.719);

}

  

.operator:active{

    background-color: hsla(35, 100%, 75%, 0.719);

  

}
