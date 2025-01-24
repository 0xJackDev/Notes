

inheritance allows a new class to inherit properties and methods from an existing class  (parent -> child)
helps with code reusability


```
class Animal{

    alive = true;

  

    eat(){

        console.log(`This ${this.name} is eating`);

    }

    sleep(){

        console.log(`This ${this.name} is sleeping`);

    }

  

}

  
  

class Rabbit extends Animal{

     name = "rabbit";

  

}

  
  

class Fish extends Animal{

    name = 'fish'

};

  
  

class Hawk extends Animal{

    name = 'hawk'

}

  

const rabbit = new Rabbit();

const fish = new Fish();

const hawk = new Hawk();

  
  

console.log(rabbit.alive);

```


this creates a Parent class named animal with a property and two methods. 

This also creates three child classes of the Animal class.

We are able to access the properties inside of Animal even through our rabbit class because it is a child of a Animal. 

To declare a child use this format 

class *Child_name* extends *Parent_name*{

}


the Rabbit hawk and fish also have access to the eat and sleep methods inside of the Parent class.

