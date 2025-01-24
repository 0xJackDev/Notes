

Today we are gonna talk about how to make lists in HTML 

we will be talking about three types of lists



Unordered Lists 
To create one of these we need a pair of ul tags 

between these <ul > tags we can create individual list items We create a pair of li (list) tags for each item in our list so if we wanted to make a grocery list of 5 items

    <h4> Unordered Lists (<ul>)</h4>

    <ul>

        <li>Pizza Cum</li>

        <li>Pizza Cum</li>

        <li>Pizza Cum</li>

        <li>Pizza Cum</li>

        <li>Pizza Cum</li>

    </ul>
    


Ordered list (<ol>)

Ordered lists are very similar but we use ol tags, and to add a item we use a pair of li tags.

The order of the list matters the It goes from Top to bottom starting at 1 so to make a ordered list 

    <h4> ordered Lists</h4>

    <ol>

        <li>          First         </li>

        <li>          Second         </li>

        <li>          Third         </li>

        <li>          Fourth         </li>

        <li>          Fifth         </li>

  

    </ol>

We can also change the type attribute in an Ordered list by in the opening ol tag adding a type= attribute. So if we set type="A" then it will count down from A, B, C, D, E and so on and so fourth down the list 



Description List (<dl>)



For this we need a pair of dl tags and instead of using an li tag for each item. We can use the dt tag for Description Term and dd tags for the description defintion. Think of the dt tag as the Title and the dd tag as the body 



  

    <h4> Description Lists</h4>

    <dl>

        <dt> Title </dt>

        <dd> Definition of title</dd>

    </dl>




you can also nest Lists inside of lists.