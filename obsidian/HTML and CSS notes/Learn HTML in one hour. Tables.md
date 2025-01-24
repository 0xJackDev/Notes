

This will show you how to make a table in html. 

Lets say we have a store and our job is to create a table of the hours of operations.


To create a table make a pair of table tags < table > 


To add a row to our table we can use a pair of tr tags for Table row.


For our example lets say we have two rows One for The days of the week and one for the hours of operation


Remember < hr > tag makes a horizontal line.


In order to make the Words inside the table row large we are gonna use the th tag or table header tag 


Table headers are auto bold. 

If we dont want to add a table Header we can add a td tag or table data tag 



<body>

    <h1>

        My Project

    </h1>

    <hr>

<table >

    <tr bgcolor="grey" >

    <th> Monday </th>    

    <th> Tuesday </th>    

    <th> Wedsnday </th>    

    <th> Thursday </th>    

    <th> Friday </th>    

    </tr>

    <tr bgcolor="lightgrey" align="center">

        <td> Close </td>

        <td> 5-9 </td>

        <td> 5-9 </td>

        <td> 5-9 </td>

        <td> 5-9 </td>

  

    </tr>

  

</table>

  
  

</body>



This is the code to create a table and it also sets the Table attributes to change the color and align the second table things into the center. 

We can also change the Width and heigh attributes


<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <h1>

        My Project

    </h1>

    <hr>

<table >

    <tr bgcolor="grey"  width="500">

    <th width="100"> Monday </th>    

    <th width="100"> Tuesday </th>    

    <th width="100"> Wedsnday </th>    

    <th width="100"> Thursday </th>    

    <th width="100"> Friday </th>    

    </tr>

    <tr bgcolor="lightgrey" align="center">

        <td> Close </td>

        <td> 5-9 </td>

        <td> 5-9 </td>

        <td> 5-9 </td>

        <td> 5-9 </td>

  

    </tr>

  

</table>

  
  

</body>

</html>


