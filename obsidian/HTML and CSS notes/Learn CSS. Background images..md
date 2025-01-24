

within our style sheet select the element in which you want the background image. like this

body{

    background-image: url(background.png);

}

with  either a relative or absolute file path 



If your image is too small then the background will repeat itself in order to make sure this doesnt happen set this property

body{

    background-image: url(background.png);

    background-repeat: no-repeat ;

}


which will make it never repeat but it will be only size of the image. 


In order to center the background image do 

body{

    background-image: url(background.png);

    background-repeat: no-repeat ;

    background-position: center;

}





you can also set the background-attachment properties, to either be fixed when you scroll or to go away when you scroll 

body{

    background-image: url(background.png);

    background-repeat: no-repeat ;

    background-position: center;

    background-attachment: fixed;

}


and there is one last property, background-size we can set this to either cover the either webpage or not. to do 

background-size: cover;


body{

    background-image: url(background.png);

    background-repeat: no-repeat ;

    background-position: center;

    background-attachment: fixed;

    background-size: cover;

}


these are good