

a function is a section of reusable code. 


to make a function type

function *functioname*(){
*code here*
}

function happybirthday(){

    console.log('happy birthday to you')

}

  

happy birthday();


this creates a function named happy birthday() and then calls it.  



pretty much works like C++ with parameters and arguments, but type function before the name instead of return type.


function add(num1, num2){

    return num1 + num2;

}

  

console.log(add(1,2));


this would log 3 to the console. There are no return types in javascript because of the Few amount of Datatypes so u can return anything from any function basically or return nothing from any function.


function isvalidEmail(email){

    if(email.includes("@")){

        return true;

    }else{

        return false;

    }

}

  

console.log(isvalidEmail('jackbuc@mail.com'))



this returns true 