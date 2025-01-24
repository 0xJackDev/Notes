

Theres two ways to do this. The easy way is to create a window prompt. 

The profession way is to make an HTML textbox of some sort and likely a button to submit the user input


Lets start with the easy way first we must create all the variables we gonna use 


let username;

user = window.prompt("What is your Username");

This will create a popup window that asks for a username. Just like a window alert popup. 

let username;

user = window.prompt("What is your Username");

console.log(user)

this will then print the username you input


Thats the easy way.



Now lets do it the professional way 


First in our HTML document lets create an input box and a submit button

<label>username: </label>

    <input id="mytext"><br> <br>

    <button id="submit"> submit </button>



When we click on the Submit button we are going to execute a javascript function first we must select this button though 
	document.getElementById("submit").onclick = 

after the = we are going to add the function in which we want to happen upon clicking the submit button element to do this we type function(){ 
*Code here*}

For example 

let username;  

document.getElementById("submit").onclick = function(){

    username = document.getElementById("mytext").value;

    console.log(username);

}

To explain this function a little. We are assigning the username variable to the value of the element my texts value and then logging that to console.


let username;

document.getElementById("submit").onclick = function(){

    username = document.getElementById("mytext").value;

    document.getElementById("content").textContent = `Welcome ${username}`;

}

This function right here will instead of logging username will search for a element named content and then change the textContent of that element to Welcome *user_var*