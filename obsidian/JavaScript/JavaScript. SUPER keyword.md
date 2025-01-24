

super is a keyword used in classes to call the constructor or access the properties and method of a parent (superclass).

this = this object
super = the parent object 



```
class Animal{

    constructor(){

  

    }

}

  

class Rabbit extends Animal{

    constructor(name, age, runspeed){

        this.name = name;

        this.age = age;

        this.runspeed = runspeed;

        }

  

}

  

class Fish extends Animal{

    constructor(name, age, swimspeed){

        this.name = name;

        this.age = age;

        this.swimspeed = swimspeed;

        }

}

class Hawk extends Animal{

    constructor(name, age, flyspeed){

        this.name = name;

        this.age = age;

        this.flyspeed = flyspeed;

        }

}

  
  

const rabbit = new Rabbit('rabbit', 12, 25);

const fish = new Rabbit('fish', 2, 12);

const hawk = new Rabbit('hawk', 3, 15);
```


if we run this we get the error script.js:9 Uncaught ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor.

This is telling us we need to call the parent objects constructor before we construct a child class of that object so we can fix this by adding super(); to the beginning of each child constructor For example fish 

  

class Fish extends Animal{

    constructor(name, age, swimspeed){

        super();

        this.name = name;

        this.age = age;

        this.swimspeed = swimspeed;

        }

}


one benefit using constructor 

