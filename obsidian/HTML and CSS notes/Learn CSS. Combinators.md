
A combinator Explains the Relationship between listed selectors 


	 *space* = Descendant
	 > = child
	 ~ = general sibling
	+ = adjacent sibling



For example take this HTML 

    <div id="container">

        <p> This is #1</p>

        <p> This is #1</p>

        <div>         <p> This is #1</p>

</div>


there is a <p > element inside of a Div element called container so in order to interact with only the paragraph that is a Descendant of Container you would use this in css

#container p{

    background-color: aqua;

}



now if you were to use the > combinator then only the first two <p > would be highlighted since the last one isnt technically a child but is a descendant since its in a seperate element. think of it as grandchildren. Paragraphs 1 and 2 are direct parents of the div container but the 3rd paragraph is a child of the Div container inside of the div container. Making it a grandchild/Descendant.


All children are descendants but not all descendants are children 




the ~ would highlight The last two paragraphs 4 and 5 since they are in the same body element both <p > and div they are siblings. But if i were to wrap both of those inside of a div section they would no longer be siblings 