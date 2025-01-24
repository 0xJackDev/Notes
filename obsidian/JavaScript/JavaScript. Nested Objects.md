nested objects are objects inside of other objects 

Allows for very complex data structures

A child object is enclosed by a parent object


const person = {

    fullName: 'Spongebob Squarepants',

    age: 30,

    isStudent: true,

    hobbies: ['karate', 'jellyfish', 'cooking'],

    address: {

        street: '123 Conch street.',

        city: 'Bikini Bottom',

        country: 'Ocean'

    }

}


for example now our person object has a nested address object inside of it. to access the address just do 

console.log(person.address.street);



