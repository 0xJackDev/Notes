
Data objects are objects that contain values that represents dates and times. These date objects can be changed and formatted for our needs


const dates = new Date();

  

console.log(dates);


this creates a new Instance of the Date object and. Since we didn't pass a value as a argument it will return Our current date and time using our system NTP.

Wed Aug 14 2024 18:08:45 GMT-0700 (Pacific Daylight Time)




if you wanna create your own data and time object pass through some args

you can follow this formula

// Date(*year*, *month*, *day*, *hour*, *minute*, *second*, *ms*))



const dates = new Date(2024, 2, 21, 2, 2, 2, 2);

  

console.log(dates);

which returns 
Thu Mar 21 2024 02:02:02 GMT-0700 (Pacific Daylight Time)

if you forget to pass through an argument it will just default to your systems time. For example if you pass through a month but nothing else it will take ur month but the rest will be ur system time 


if you need the Month you can do 


const date = new Date();

  

const month = date.getMonth();

  

console.log(month)


or for seconds you could do 


const Seconds = date.getSeconds(); 



of you can use getFullyear to get the full year

so on so fourth. for Day, seconds, Minutes, 



instead of get if you want to set a specific one you can use 

.set 

for example

date.setMonth(0); would set the month to 0. 