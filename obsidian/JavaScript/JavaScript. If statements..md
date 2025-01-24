

let age = 25;

  

if(age >= 25){

    console.log("Allowed");

}else{

    console.log("BANNED");

}

if statements work alottt like C.


Indentation is important for nested if statements.


there is also else if statements 



if(age >= 25 && age < 101){

    console.log("Allowed");

}else if(age < 0){

    console.log("Your age cant be below 0");

}else if (age >= 101){

    console.log("you are too old");

}else{

    console.log('you are too young to enter this site')

}


&& is AND so if age is greater or equal to 25 AND age is less then 101. 


submitbtn.onclick = function(){

    age2 = input.value;

    if(age2 >= 25 && age2 < 101){

        text.textContent = `Congrats you are allowed in your age is ${age2}`;

    }

    else if(age2 > 100){

        text.textContent = `DENIED you are too old your age is ${age2}`;

    } else if(age2 < 0){

        text.textContent = `ERROR CANT ENTER NUMBER LOWER THEN 0`;

    }else{

        text.textContent = `DENIED YOU ARE UNDER 25 Your age is ${age2}`;

    }

    }