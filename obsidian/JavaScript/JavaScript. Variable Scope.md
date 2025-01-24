

Variable scope is where a variable is recognized and accessible (local vs global)



Any variable declared inside of a function has a local scope.  Meaning it is only Recognized and accessible within that function it has been defined in 



Functions cant see inside of other functions. 



A global scope is any variable declared outside of a function. And these elements can be accessed from anywhere within your program. Even within other functions.



if we have two variables with the same name and they are in different scopes we will use the local version first instead of the global version. If the local variables arent available then you would use global. 