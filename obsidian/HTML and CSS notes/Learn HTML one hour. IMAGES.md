

Okay party people. This is how to add a image to a webpage.


We will use shrek.png for this.


Within the folder containing your index.html file, "or whatever html file you are in which needs to access the image" move or paste that file into that directory.


and wherever within the body element we will create a new element. The image element, type 

	<img>


and we will need a source attribute of this image element. and we want to set this equal to the name of the image so


	<img src="shrek.png">



you dont really need to have it in the same directory but if you dont you need to have the full directory so that the html file can reach it. remember this is the relative directory not Root. Create a images folder inside your html folder.


We can do more with the width and height of this image working with the attributes for example

	<img src="shrek.png" height="300" width="100">

if someones visually impared you can have something that will read out loud text by a screen reader. so that is the alt attribute so 

alt="This is a picture of shrek"

you can also add a title popup box with title= attribute.



we can also turn a image into a hyperlink to do this we need to surrond our image elements with <a > tags 


dont foget target=blank attribute inside of the <a hyperlink > though so it opens in new tab 