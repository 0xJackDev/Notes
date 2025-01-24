
a constructor is a special method for defining the properties and methods of objects 

function Car(make, model, year, color){

    this.make = make,

    this.model = model,

    this.year = year,

    this.color = color

}

  

const car1 = new Car('ford','fusion',2017,'red');

  

console.log(car1.make);


this creates the Constructor Function Car and then we make a new instance of the Car Object by assigning a variable to it and type the new keyword then the functions name and then the arguments we want as properties in our new object then we could create multiple car objects. with all the same properties but different values in those properties. 