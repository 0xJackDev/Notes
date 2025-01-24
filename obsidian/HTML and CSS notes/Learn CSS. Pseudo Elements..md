

A pseudo element is a keyword added after a selector thats used to style a specific parts of an element.



You have a slector for example h1 then :: and then the pseudo element for example

selector::pseudo-element {

}


h1::first-letter{

}


For example to make every first letter in each List element Large do this.

li::first-letter{

    font-size: 2em;

}


To change any text that is select/highlighted inside of any paragraph element to green to this

p::selection{

    color:green;

}

Now anything you highlight text will be green if you wanted tgo change the background color as well you could 


to add a checkmark marker to each item in the List called fruit do this 


#fruit li::marker{

    content: "✔️"

}




The difference between elements and classes, Is A pseudo class modifies the behavior of a selector with : while a Pseudo element Allows for styling of an element or adding parts to a selector using ::