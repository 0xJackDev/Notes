

a switch can be an efficient replacement to many else if statements 

let day = 1;

  
  

switch(day){

    case 1:

        console.log("It is monday");

        break;

    case 2:

        console.log('it is Tuesday');

        break;

}



Look at this. In this we are using the switch() function. we put the variable we want to examine there.
In case 1 we are checking that in the first case if it equals 1 then do this Console.log it is monday. But if the case is == 2 then console.log it is Tuesday


let day = 'WhatsUp';

  
  

switch(day){

    case 1:

        console.log("It is monday");

        break;

    case 2:

        console.log('it is Tuesday');

        break;

    case 'WhatsUp':

        console.log(222);  

}



As you can see i can set the value after case to be anything with this script above it will output 222 to the console. 

there is also a default: which is triggered when there isnt a case that matches what the variable is. 

  

let day = 'pizza';

  
  

switch(day){

    case 1:

        console.log("It is monday");

        break;

    case 2:

        console.log('it is Tuesday');

        break;

    case 3:

        console.log('it is Wednesday');

        break;

    case 4:

        console.log('It is Thursday');

        break;

    case 5:

        console.log('it is friday');

        break;

    case 6:

        console.log('it is saturday');

        break;

    case 7:

        console.log(' it is sunday');

        break;

    default:

        console.log('error No matches')

}

This would log error with no matches.

Instead of you Don't have a match without a default case then it will simply exit the switch without triggering any code.


Its important to use break after every code snippet is so that we break out of the switch once we have a matching case. If you do not have this then once we have a matching case it will execute all of the lines of code AFTER the case sequentially including other cases after unless we have a break. 


