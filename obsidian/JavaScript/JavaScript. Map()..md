

the .map() method accepts a callback and applied that function to each element of that array and then returns a new array.  Almost exactly like the forEach() method but it creates a new array instead of editing the existing one 


const numbers = [1,2,3,4,5,6];

  
  

function square(element){

    return Math.pow(element,2);

}

let newarray = numbers.map(square)

  

console.log(newarray)


this creates a new array called new array which is all the elements of Numbers squared returns 
1. 0: 1
2. 1: 4
3. 2: 9
4. 3: 16
5. 4: 25
6. 5: 36




const dates = ["2024-1-10", '2025-2-20', '2020-3-30'];

  

const formatteddates = dates.map(FormatDates);

  

console.log(formatteddates)

  

function FormatDates(element){

    const parts = element.split('-');

    return `${parts[1]}/${parts[2]}/${parts[0]}`

}



this is more practical it makes a function that splits the dates and then reformats then going from Day Month year 