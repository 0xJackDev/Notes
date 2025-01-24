

string slicing is the process of creating a substring from a portion of another string.


for example. string.slice(*start*, *end*);


The ending index is exclusive you dont include the ending index. 

for example to split the String Bro Code into just a string called bro you would do 

const fullname = "Bro Code";

let firstname = fullname.slice(0,3);

console.log(firstname);



const fullname = "Bro Code";

let firstname = fullname.slice(0,3);

let lastname= fullname.slice(4);

console.log(lastname);


if you are gonna create substring all the way starting at the starting index till its finished you dont need an ending index. 



to get the firstchar use .slice(0,1);


if you wanna get the last char in a index just use .slice(-1); which will return the last letter. 

negative numbers reverse the index so if you were to do -2 it would get the last two chars but in order of Right to left. 


to make string slixing more dynamic we can use it with the indexof method 

say we want to search for the first instance of a space and split it. 

const fullname = "Broseph Code";

let firstname = fullname.slice(0, fullname.indexOf(" "));
let lastname = fullname.slice(fullname.indexOf(" ") + 1);

console.log(firstname);

this would print broseph and make code a seperate varaible named last name. and we add the +1 so it starts at the index after the space and doesnt print the whitespace. 



const email = 'jackbuc@gmail.com';

  

const username = email.slice(0, email.indexOf('@'));

const mail = email.slice(email.indexOf('@'));

  

console.log(username);

console.log(mail);


this would split a email into a username and mail carrier pieces separating at the @ symbol 