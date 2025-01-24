
to change the font style go to our css style sheet and select which element you want to change by setting the font-family attribute for example if i wanted to change the h1 header i could do


h1{

    font-family:Verdana;

}

it is good practice that in case a browser cannot load one font to set multiple fonts as a fall back incase the first doesnt work in the browser for example. 


h1{

    font-family:Verdana, arial, Courier;

}





if the font name contains any spaces put the font name within quotes "" 





we can also change the font-size attribute you can use either pixels or em in order to measure this. think of 1em as 100% or the normal size and 1.1em would be 110%. 2em = 200%. 

You can also use pixels 

h1{


    font-size:2em;

}


that is all for basic fonts, now we will introduce google fonts.




first go to fonts.google.com and find a font. and click get embed code. 

Copy the <link> that it gives you and put it in the head of your html document. After we pasted the link like this

<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <link rel="stylesheet" href="style.css">

    <link rel="preconnect" href="https://fonts.googleapis.com">

<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<link href="https://fonts.googleapis.com/css2?family=Anton+SC&display=swap" rel="stylesheet">

    <titlwerewrDocument</title>

  

</head>



We can now use the google font by simply going into the external css file and using the name of the google font we just linked. For example we just downloaded "Anton SC"  


h1{

    font-family:"Anton SC";

    font-size:2em;

}.


Thats how you use the google fonts api they cant be locally loaded or loaded from a server but im not gonna write how to do allat cause i dont think its useful  but all you really need to do is somehow download the .ttf file of the font and then drag it into the folder where you wanna use it then in the css file you wanna use it in you must declare a font face do it like this

@font-face{
	src: url(*relative path to .ttf file");
	font-family: *Desired name of font*;
}
