

In order to create a form we need an opening and closing Form tag 

	<form> </form>

In order to create a input field inside this we need to add a input tag for example

	<input type="text"> 
we can set the type to whatever we wanna input, for example text or number.

We probaly want to tell the user what to put in this box and give it a label if we wanna do this in the line before add the label tags.  to add a label. It is considered good practive to add a for attribute inside of a label, This should be equal to the id attribute that you need to have in your input tag. For example

	<label for="fname>
	<input type="text" id="fname">



You could also add a placeholder attribute inside of the input element placeholder= to have some text in the box but that text will disseaper once you click on it 


	in forms there is also built in buttons like you can set <input type="reset"> and it will make a reset button that resets the forms




also if you want to to have two different input boxes But dont want it inside of the same form then you can use < div >




In forms theres another built in button if you set the input type="submit" it sends the data.

Currently we have no where for this data to go so if we click submit nothing will happen with it. So if i need to send this data to a parge I will add this page within the form element with the action attribute.


We will need the help of a dynamic programming language for this, php for example. 

For example if i was needing to send this to a php page it would be 

	<form action="action_page.php">

There is also a method associated with this action attribute. Two common values are GET and POST. Get is considered insecure, it simply appends your data to the URL of your webpage.  for example if i set the method to get when i click the button my URL will be.


If you need to transport information like Passwords do not use get.

GET is useful for things like search boxes.



There is also a required attribute you can add that makes it required for someone to submit some type of information to be able to submit the form.




Next we have password fields


for an email element set the type as email.




for a telephone number set the type="tel" 





If you need the user to type in a date you can set the type date.





There is also a number type. We should set the min and max attributes for this though so they cant just use as big of a number as possible so add min=0 and max=99 or whatever you want it to.





Radio buttons.

With radio buttons you can only select one out of the group. Are you a mr a Mrs. Or a Doctor?



If you want a dropdown menu instead of having  an input tag we will have a pair of select tags.

And we list indivual option tags inside of this element for example for paying with three different options



    <label> Payment</label>

    <select>

        <option> Visa</option>

        <option> Mastercard</option>

        <option> Express</option>

  

    </select>






The last type i will talk about is the checkbox type which is how it sounds a checkbox.




there is also a file type and a comment type. 


for the file type you can choose to only accept files of certain types with the accept= attribute.



If we are allowing sending large images we need to change the encryption type in our form to enctype="multipart/form-data" so it encrypts and sends it in multiple parts 