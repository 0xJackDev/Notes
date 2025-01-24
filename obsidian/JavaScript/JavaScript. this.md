

this is a keyword.

this = a reference to the object where THIS is used (the object depends on the immediate context)

for example if we had a object named person with a property named name we could replace person.name with this.name as long as we are working within this object.

const person = {

    firstName: "spongebob",

    LastName: "squarePants",

    age: 30,

    isEmployed: true,

    sayHello: function(){console.log(`Hi my name is ${this.firstName}`)},

}


i have to add the this.firstname so it knows its grabbing the property inside of THIS object if i just had Firstname it wouldn't work! it would be the same as saying person.firstName though


the this keyword doesnt work with arrow functions