

props which is short for properties are read only properties that are shared between components. A parent component can send data to a child component.

Using props we can send an individual component so they are all unique 


For example 

this is students.jsx

```
  
  
  

function Student(props){

    return (

        <div>

            <p>Name: {props.name}</p>

        </div>

    );

}

  

export default Student
```

You see how we have to pass through a value to the Student function. Well that value will be name. Look how we do this


```
import Student from "./students/students.jsx";

  
  

function App() {

  return(

    <Student name="John"/>

  );

}

  

export default App
```

As you see we use the key which is in this case name= to pass through the name john and print name: John. So in order to get the associated value you will type *name_of_argurment*.*key_name* like props.name in this case!


now say you wanna pass through age. Since it is not a string literal you wanna use the curly braces since its a integer. 

```
import Student from "./students/students.jsx";

  
  

function App() {

  return(

    <Student name="John" age={23}/>

  );

}

  

export default App
```




```
  
  
  

function Student(props, age, isStudent){

    return (

        <div>

            <p>Name: {props.name}  Age: {props.age} IsStudent={props.isStudent ? "Yes" : "No"}</p>

        </div>

    );

}

  

export default Student
```


since IsStudent is a True or false we have to Have two things to return so based on this i am using the tenary operator so It is a easy fix. 




proptypes is a mechanism that ensures that the passwd value is of the correct datatype for example we wanna ensure the age value is a number. 

So heres how we do this after the Student function we will create a propTypes like this 

First we have to import proptypes 


```
  

import PropTypes from 'prop-types'

  

function Student(props, age, isStudent){

    return (

        <div>

            <p>Name: {props.name}  Age: {props.age} IsStudent={props.isStudent ? "Yes" : "No"}</p>

        </div>

    );

}

  

Student.PropTypes = {

    name: PropTypes.string,

    age: PropTypes.number,

    isStudent: PropTypes,

}

  

export default Student
```