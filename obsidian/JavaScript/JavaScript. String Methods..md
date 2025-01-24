

string methods allows you to manipulate and work with strings.


Suppose i would like to get the first character of this string i can use the .charAt method. 

let username = 'stix';

console.log(username.charAt(0));

this would log s to the console since its the in the 0th place. If you were to change this 0 to a 1 it would log to letter t. So on so fourth. Just remember in lists 0 = 1



the .indexOf method looks for the first instance of a letter for example if i wanted to look for the first instance of the letter i. i could do this

let username = 'stix';

  

console.log(username.indexOf('i'));


which would return 2 because I is at the 2nd place in the list. 'technically third'.


to find the last instance of something use the .lastIndexof function.


to get rid of any whitespace in a string use the .trim Function 



to make everything uppercase use the .toUpperCase(); method

and there's to .toLowerCase(); method which guess what! makes it all lowercase 




to determine if a string starts with a certain character we can use the .startsWith method which will return a boolean. 


For example if we wanted to check if a string started with a emptey space we can do

let username = 'stix';

  

console.log(username.startsWith(' '));


which returns false but if i add a space before the S in stix it will return True 



there is also the .endsWith(); Method which is like starts with but checks the end.


there is also there .includes(); method which check if the string contains something. Returns either true or false.





.replaceAll(); method will replace any specific characters with another. For example say we had a phone number and wanted to get rid of the - and replace them with nothing you can do. 

let phonenumber = '842-222-2222';

phonenumber = phonenumber.replaceAll('-', '');

console.log(phonenumber);


this would return the phone number with no dashes



there is also the .padStart(); method the first parameter of this is how long you want a string to be and the second is what character we want to pad with. say we only had 11 chars in our string but we set .padStart(15, '0')

then the first four chars would be  0000 since it needs to be 15 characters long.



.padEnd(); does the same thing but instead of adding the padding at the beginning you add it at the end 