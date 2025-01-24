

em adjusts the size depending on the parent element rem adjusts the size based on the root. thats why its Rem.

function rolldice(){

    const numofdice = document.getElementById('inputelement').value;

    const diceresult = document.getElementById('diceResult');

    const diceimages = document.getElementById('diceimages');

    const values = [];

    const images = [];

  

    for(let i = 0; i< numofdice; i++){

        const value = Math.floor(Math.random() * 6) + 1;

        values.push(value);

        images.push(`<img src="side${i}.png" alt="Dice ${value}">`)

    }

  

    diceresult.textContent = `dice: ${values.join(', ')}`;

    diceimages.innerHTML = images.join('');

    console.log(values);

}



<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

    <link rel="stylesheet" href="style.css">

</head>

<body>

    <div id="container">

        <h1> Dice Roller</h1>

        <label># of dice:</label>

        <input type="number" value="1" min="1"   id="inputelement">

        <button onclick="rolldice()"> Roll dice</button>

        <div id="diceResult"></div>

        <div id="diceimages"></div>

    </div>

    <script src="script.js"></script>

</body>

</html>
#container{

    font-family: sans-serif;

    text-align: center;

    font-size: 2rem;

    font-weight: bold;

  

}

  

button{

    font-size: 1.5rem;

    padding: 10px 15px;

    border-radius: 10px;

    border: none;

    background-color: hsl(240, 100%, 53%);

    color:white;

    font-weight: bold;

    cursor: pointer;

}

  

button:hover{

    transition: .5s;

    background-color: rgb(90, 90, 250);

}

  

button:active{

    transition: .2;

    background-color: hsl(199, 100%, 74%);

}

  
  

input{

    font-size: 2rem;

    width: 150px;

    text-align: center;

    font-weight: bold;

}

  

#diceResult{

    margin: 25px;

}

  

#diceimages img{

width: 100px;

height: 100px;

  

}