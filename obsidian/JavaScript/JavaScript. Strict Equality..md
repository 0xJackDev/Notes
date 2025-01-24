

the strict equality operator is === and it compares if values AND datatypes are equal


= is the assignment operator

== is the comparison operator which ONLY compares the values to see if they are equal

=== is the strict equality operator


!= is the inequality operator

!== is the strict inequality operator 


const PI = 3.14;

  

const PIstr = '3.14';

  

if(PI === PIstr){

    console.log('data type and value is the same');

}else if(PI == PIstr){

    console.log('Data type is different but value is the same');

}else{

    console.log('different data type and value');

}


This would print Data type is different but value is the same. 
