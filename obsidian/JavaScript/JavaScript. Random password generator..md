

  
  

```
function generatePassword(length,

                        includeLowercase,

                        includeUppercase,

                        includeNumbers,

                        includeSymbols){

    const lowercasechars = 'abcdefghijklmnopqrstuvwxyz';

    const uppercasechars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';

    const numberchars = '0123456789';

    const symbolschars = '!@#$%^&*()';

  

    let allowedchars = "";

  

    let password = "";

  

    allowedchars += includeLowercase ? lowercasechars : "";

    allowedchars += includeUppercase ? uppercasechars : "";

  

    allowedchars += includeNumbers ? numberchars : "";

  

    allowedchars += includeSymbols ? symbolschars : "";

  

    if(length <= 0){

        return `(password length must be at least 1)`;

    }

  

    if(allowedchars.length === 0){

        return '(at least set of characters needs to be selected)';

    }

  

    for(let i = 0; i < length; i++){

        const randomindex = Math.floor(Math.random() * allowedchars.length);

        password += allowedchars[randomindex];

    }

    return password;

}

  

password = generatePassword(15,true,true,true,true);

  
  
  

console.log(`Generated password: ${password}`);




```