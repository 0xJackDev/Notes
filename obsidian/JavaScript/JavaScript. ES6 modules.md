


a module is an external file that contains reusable code that can be imported into other javascript files. Can contain variables, classes, functions and more 


for example lets create a separate Mathutil.js file. 

in order to add this in our index.html file we must set this for this 

    <script type="module" src="script.js"></script>
now we can import and export files freely into our script.js file 


this is whats in our mathUtil.js File


  
```

export const PI = Math.PI;

  
  

export function GetCircumfrence(radius){

    return 2 * PI * radius;

}

  

export function GetArea(radius){

    return PI * radius * radius;

}

  

export function getVolume(radius){

    return (4/3) * PI * radius * radius;

}
```



as you can see we put the export keyword before any function or variable we wish to export into anothe file. now in my script.js file to import this we can do. 


import {PI, GetCircumfrence, GetArea, getVolume} from './mathUtil.js';

  

console.log(PI);


as you can see in the import part we use object Destructuring and type in all the variables and function OUIs that we want to use in our script.js File. I then log the value of PI to the console. and it works 