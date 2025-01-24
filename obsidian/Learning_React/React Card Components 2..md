

A react component is a reusable section of JSX code. Which is HTML like code that can contain javascript.


Lets create some card coomponents. Which typically have a picture, a title and description.


IN JSX class is a reserved keyword to set a class of a HTMLx tag use className. 


In order to use a picture inside of your react element you must first import it into the Source file in which the element is. For example. 

```
import profilePic from './assets/Picture.png'

  
  

function Card(){

    return(

        <div className="card">

            <img alt="profile picture" src={profilePic}></img>

            <h2>Jack Buchanan</h2>

            <p>I am a Information Security researcher.</p>

        </div>

    );

}

  

export default Card;
```

