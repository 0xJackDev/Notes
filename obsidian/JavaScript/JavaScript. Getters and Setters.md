

getter is a special method that makes a property readable {get Keyword}

setters is a special method that makes a property writable {set Keyword}

we can use getters and setters to validate and modify a value when reading/writing a property.



class Rectangle{

  

    constructor(width, height){

        this.width = width;

        this.height = height;

    }

  

    set width(newWidth){

        if(newWidth > 0){

            this._width = newWidth;

        }

        else{

            console.error('width must be a postive number');

        }

    }

}

  
  

const rectangle = new Rectangle(-100000000, 'pizza');

  

console.log(rectangle.width)

this will return 
script.js:13 width must be a postive number


since we do some validating with this 
    
    
    set width(newWidth){

        if(newWidth > 0){

            this._width = newWidth;

        }

First we set the value of newWidth to width then we check if newWidth is less then 0. If it is then we will log an error if it is not then we will set the private class this._width to equal Newwidth. the _ tells other devs that this is a private property and not to be changed.



class Rectangle{

  

    constructor(width, height){

        this.width = width;

        this.height = height;

    }

  

    set width(newWidth){

        if(newWidth > 0){

            this._width = newWidth;

        }

        else{

            console.error('width must be a postive number');

        }    

    }

    set height(newHeight){

        if(newHeight > 0){

            this._height= newHeight;

        }

        else{

            console.error('height must be a postive number');

        }

}

}

  

const rectangle = new Rectangle(-100000000, 'pizza');

  

console.log(rectangle);


this code returns 
script.js:13 width must be a postive number
set width @ script.js:13
Rectangle @ script.js:4
(anonymous) @ script.js:26Understand this error
script.js:21 height must be a postive number

and so we cant set a value to anything but a positive number. But even if we do change it do a positive number in the code above it still wont work. That's because these properties are writeable via setters but not readable. That's where getters come in. 


class Rectangle{

  

    constructor(width, height){

        this.width = width;

        this.height = height;

    }

  

    set width(newWidth){

        if(newWidth > 0){

            this._width = newWidth;

        }

        else{

            console.error('width must be a postive number');

        }    

    }

    set height(newHeight){

        if(newHeight > 0){

            this._height= newHeight;

        }

        else{

            console.error('height must be a postive number');

        }

}

    get width(){

        return this._width;

    }

    get height(){

        return this._height;

    }

}

  

const rectangle = new Rectangle(3, 3);

  

console.log(rectangle);



now this code here will work. The reason we need the get is because once we use the set to do the checking to make sure we actually change the variable/property to another private propety name _height or _width. 

with getters we can also return propertys or variables that dont exist for example we could do 

    get area(){

        return this._width * this._height;

    }
and then we can access the rectanglee.area property as if it was a normal propety with.

console.log(rectangle.area);


our area isnt techinally a property but we can access it as if it was one because of a getter. 


basically 

    get width(){

        return this._width;

    }
   we are returning the value width to equal the private value this._width so it can be accessed globally  