

while loop repeats some good WHILE a condition is true.


 Lets say we wanted to make a window prompt that would only go away once a user entered a username
let username = ''

  

while(username === ''){

    username = window.prompt('Please enter your username');

}

  

console.log(`Hi ${username} Welcome`);

This wouldnt let me click out of the window prompt UNTIL i entered the username Because it will keep opening one until the username variable gets assigned away from an empty string.


A while loop simply repeats code until a condition is not true.

if you press the cancel button username will equal NULL so change the while loop to

while(username === '' || username === null){

    username = window.prompt('Please enter your username');

}


there is also another variation of a while loop known as a do while loop for example i could change the code to 

let username;

  

do{

    username = window.prompt('Please enter your username');

}while(username === '' || username === null)

  

console.log(`Hi ${username} Welcome`);

while will do     username = window.prompt('Please enter your username'); WHILE while(username === '' || username === null). This just allows you to move your condition to the end.


where you do the code first then check the condition after.


let loggedin = false

let username;

let password;

  

while(!loggedin){

    username = window.prompt("please enter a username");

    password = window.prompt("Please enter your password");

  

    if(username == "John" && password == "Password"){

        loggedin = true;

        console.log('You have logged in');

    }else{

        loggedin = false;

        console.log('Invalid Credentials');

    }

  

}


with this above it will repeat as long as loggedIn is not TRUE. and it will only set loggedin to true if you have the correct username and password 