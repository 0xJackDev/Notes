

body{

    margin: 0;

    background-image:url('background.jpg');

    background-position: center;

    background-repeat: no-repeat;

    background-size: cover;
       background-attachment: fixed;

}

  
  

#clockcontainer{

    display:flex;

    justify-content: center;

    align-items: center;

    border:2px solid;

    height: 100vh;

}

  

#clock{

    font-size: 6.5rem;

    font-family: monospace;

    text-align: center;

    font-weight: bold;

    color: hsl(0, 1%, 63%);
        backdrop-filter: blur(5px);

    width:100%;

    background-color: hsla(0, 0%, 50%, 0.075);

  

}



Here is the CSS for everything. the background part is important to remember 

    background-size: cover;

this makes sure that the background shows the whole picture and scales when u change the browser size. and doesnt look weird and the think about no repeat makes sure it doesnt repeat too. 



const clockcontainer = document.getElementById('clockcontainer');

const clock = document.getElementById('clock');

  
  

function updateClock(){

    const now = new Date();

    const hours = now.getHours();

    const minutes = now.getMinutes();

    const seconds = now.getSeconds();

    const timestring = `${hours}:${minutes}:${seconds}`;

    clock.textContent = timestring;

}

  

updateClock();

  

setInterval(updateClock,1000);



the setInterval function makes it so this function will get called every 1000 ms or once a second. 