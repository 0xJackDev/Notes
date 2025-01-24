

To create a react framework with all the files you will need type this


npm create vite@latest

this is inside Header.jsx
```
function Header(){

  

    return (

        <header>

            <h1> my website</h1>

        </header>

    );

}

  

export default Header
```

Inside of the return (); block you can type HTML elements. The return element is only capable of having one Element be returned, but you can place children elements underneath the first. 


Now if i want to call a instance of this header component Inside of  app.jsx You must call an instance of the Header class to render it. Like so.

app.jsx
```
import Header from "./Header.jsx"

  

function App() {

  

  return(

    <Header></Header>

  );

}

  

export default App
```

Now main.jsx will render app.jsx to the virtualDOM i believe.


The reason we export the App function at the bottom is so we can use it elsewhere in other code files. 

Lets make a footer file. 

```
  

function Footer(){

    return(

        <footer>

            <p>&copy; Zerothreat</p>

        </footer>

    );

  
  

}

  

export default Footer
```



Now include this in your App.jsx and you get an error since Return can only return One HTML element and you are trying to return two Both header and footer. To fix this we need to make a JSX fragment. So we enclose our components in whats called a fragment or a set of empty angle brakets like this <> </>

```
import Header from "./Header.jsx"

import Footer from "./footer.jsx";

function App() {

  

  return(

    <>

    <Header/>

    <Footer/>

    </>

  );

}

  

export default App
```

And this works!


now back to our footer.jsx file. Lets insert some javascript inside our return statement. To insert javascript you need a set of {}.


```
  

function Footer(){

    return(

        <footer>

            <p>&copy;{new Date().getFullYear()} Zerothreat</p>

        </footer>

    );

  
  

}

  

export default Footer
```

This footer element will now show ©2024 Zerothreat.


Now lets create a Unordered list So we can put it between our Header and footer. 