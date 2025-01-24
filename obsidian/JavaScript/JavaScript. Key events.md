
an event listener can also listen for Interactive key events In this we will be discussing 'keydown' and 'keyup' there is a third type of key event called 'keypress' but according to the documentation its not capatible with all web browsers so you should avoid using it. 


Keydown makes something happen when you press down on a key and keyup makes something happen when you release 


document.addEventListener('keydown', event =>{

    console.log(event);

})

this function will log what key is pressed for example if i press d then it will log upon d being pressed.
KeyboardEvent {isTrusted: true, key: 'd', code: 'KeyD', location: 0, ctrlKey: false, …}


document.addEventListener('keyup', event =>{

    console.log(event);

})


this will log the exact same thing but will trigger once a key is released, not pressed



const mybox = document.getElementById('mybox');

  

document.addEventListener('keyup', changeText);

  

function changeText(event){

    mybox.textContent = 'boos';

}


this would change the html document of 



const mybox = document.getElementById('mybox');

  

document.addEventListener('keyup', changeText);

  

function changeText(event){

    try{

    if(event.key === 'd'){

        mybox.textContent = 'd';

    }

    else{

        mybox.textContent = 'Char other then d pressed';

  

    }    

}

    catch(error){

        console.log(error);

    }

  

}


this would check the key pressed and if it is 'd' then we will change the content of an HTML element to d if not we change it to char other then d pressed