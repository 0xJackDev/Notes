
Classes are an ES6 feature that provide a more structured and cleaner way to work with objects compared to the traditional constructor functions.



to create a class you type class then the name of the object 

to create a constructor inside of a class use the constructor keyword as with the parameters being inside () then do it normally.

you dont have to use the function keywords inside of a class. 


  

class Product{

    constructor(name,price){

        this.name = name,

        this.price = price;

    }

  

    displayProduct(){

        console.log(`Product: ${this.name}`);

        console.log(`Price: ${this.price}`)

  

    }

}

  

const product1 = new Product("Shirt", 19.99);

  

product1.displayProduct();


this creates a class named product with a constructor to create a product with two properties. Then also makes a function to display these Two properties and then we define a new instance of an object and then call the function displayProduct(); 