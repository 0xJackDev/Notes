Static is a keyword that defines properties or methods that belong to a class itself rather than the objects created from that class (class owns anything static, not the objects)


class MathUtil{

    static PI = Math.PI;

  

}

  

console.log(MathUtil.PI);

this creates a static variable inside of the Class MathUtil that we then access the PI variable inside of this class. Without creating an object 


class MathUtil{

    static PI = Math.PI;

  

    static getDiamter(radius){

        return radius * 2;

    }

  

}

  

console.log(MathUtil.PI);

console.log(MathUtil.getDiamter(2));


this creates and uses a function to get diameter  ya get the point. Make sure to use the static keyword if you are making a static property inside class.



  
```

class User{

    static userCount = 0;

  

    constructor(username){

        this.username = username;

        User.userCount++;

    }

}

  

const user1 = new User("Spongebob");

const user2 = new User("Patrick");

const user3 = new User("Sandy");

```
  
  

console.log(User.userCount);

this would log three to the console as we have three seperate user objects 