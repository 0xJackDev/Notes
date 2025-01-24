
an object is a collection of related properties and or methods.
Properties are things that a person has like First name or lastname a method is a function that belongs to a object 

  

const person = {

    firstName: "spongebob",

    LastName: "squarePants",

    age: 30,
    isEmployed: true,



}


this makes an object named person that has four properties inside of it Firstname, lastname and age and isemployed. notice how after the Property we put : instead of = to assign a value and we separate each property with a comma after ,


In order to interact with a property use this format 
*object*.*property* 

so to log the age of the person lets do this 

console.log(person.age);



Objects cant have the same name. They need a unique OUI or Object Unique Identifier :3.

lets create a function inside of our person object

const person = {

    firstName: "spongebob",

    LastName: "squarePants",

    age: 30,

    isEmployed: true,

    sayHello: function(){console.log('Hi! i am Spongebob!')}

  

}

make sure not to put a semicolon ; at the end of anything. So you see all the syntax for assigning something is the same just type function() afterwards to make it a function and to call it you can do 

person.sayHello();
