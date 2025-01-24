
Method chaining is a programming technic where you call one method after another in one continuous line of code. 


a program that doesnt use method chaining that would get the first char of a string and make it uppercase and make the rest of it lowercase without anywhitespace would look something like.
  

let username = window.prompt("please enter a username: ")

username = username.trim();

let firstchar = username.charAt(0,1);

firstchar = firstchar.toUpperCase();

let extrachar = username.slice(1);

extrachar = extrachar.toLowerCase();

username = firstchar + extrachar;

console.log(username);


This program does work but its alot to write. With method chaining we can combine some of these steps together and get rid of variables we don't need. 


Here is the same program using method chaining

let username = window.prompt("please enter a username: ")

  

username = username.trim().charAt(0).toUpperCase() + username.trim().slice(1).toLowerCase();

  

console.log(username);


as you can see after one method we can use . instead of ; so that after that method is done we perform the method to the write. It processes these from left to right. 