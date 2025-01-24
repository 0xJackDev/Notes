
Lets say you are driving to a friends house for the first time, and the address given to you is 245 front street in mill city. Upon reaching mill city you take out your map only to discover that mill city has two different front streets across town from each other! Which one would you go to? unless there was some additional information to help you decide you'd have to call your friend and ask for more information. because this would be confusing and inefficient in most countries all street names and house addresses within a city are required to be unique.

Similarly, C__ requires that all identifier be non-ambiguous. If two identical identifiers are introduced into the same program in a way that the compiler or linker cant tell them apart this will produce an error called a naming collision error. or naming conflict.

If the colliding identifiers are introduced into the same file, the result will be a compiler if colliding identifiers are introduced into separate files belonging to the same program it will result in a linker error.

Here's an example of an naming collision 

a.cpp file: 
#include <iostream>

void myFcn(int x)
{
    std::cout << x;
}


main.cpp file:

#include <iostream>

void myFcn(int x)
{
    std::cout << 2 * x;
}

int main()
{
    return 0;
}

-------

When the compiler compiles the program, it will compile a.cpp and main.cpp independently, and each file will compile with no problems

However when the linker executes it will link all the definitions in a.cpp and main.cpp together and discover conflicting definitions for the function myFcn() as it has the same name and parameters. The linker will then abort with an error. Note that this error occurs even though myFcn() is never called!

Most naming collisions occur in two cases:
1. Two (or more) identically named functions or global variables are introduced into separate files belonging to the same program. This will result in a linker error as shown above
2. Two (or more) identically named functions (or global variables) are introduced into the same file. This will result in a compiler error.

As programs get larger and use more identifiers, the odds of a naming collision being introduced increases significantly. The good new is that C++ provides plenty of mechanisms for avoiding naming collisions. Local scope, which keeps local variables defined inside functions from conflicting with each other, is one such mechanism. But local scope doesn't work for function names. So how do we keep function names from conflicting with each other?  

Scope regions.

Back to our address analogy for one moment, having two front streets was only problematic because those streets existed within the same city. On the other hand if you had to deliver mail to two addresses, one at 245 front street in mill city and another at 417 front street in jonesville. There would be no confusion on where to go. Put another way cities provide groupings that allows us to make sense of addresses that might otherwise conflict with each other.

A scope region is an area of source code where all declared identifiers are considered distinct from names declared in other scopes (much like cities in our analogy). Two identifiers with the same name can be declared in separate scope regions without causing a name conflict. However within a given scope region all identifiers must be unique otherwise naming collision will result.

The body of a function is one example of a scope region. two identically named identifiers(variables) can be defined in separate functions without issue -- because each function provides a separate scope region, there is no collision however if you try to define two identically named identifiers(variables) within the same function, a naming collision will result and the compiler will complain.

Namespaces

A namespace provides another type of scope region (called namespace scope) that allows you to declare names inside of it for the purpose of disambiguation "making something clear for the compiler/linker". Any names declared inside the namespace wont be mistaken for identical names in other scopes

!insight. A name declared in a scope region (such as namespace) wont be mistaken for another  name declared in another scope.

Unlike functions which are designed to contain executable statements, only declarations and definitions can appear in the scope of a namespace. For example two identically named functions can be defined in separate namespaces and no naming collision will occur.

Key insight. Only declarations and definitions can appear in the scope of a namespace (not executable statements) . However a function can be defined inside a namespace and that function can contain executable statements inside of it

Namespaces are often used to group related identifiers in a large project to help ensure they dont collide with other identifiers. For example if you put all your math functions in a namespace named math, then your math functions wont collide with identically named functions outside of the math namespace

We will learn how to create your own namespaces in a future lesson

The global namespace

In C++, any name that is not defined inside a class, function, or namespace is considered to be part of an implicitly-defined namespace called the global namespace (sometimes refered to as global scope)

In the example at the top of the lesson, functions main() and both version of myFcn() are defined in the global namespace. The naming collosion encountered in the example happens because both versions of myFcn() end up inside the global namespace, which voilates the rule that all names in a scope region must be unique.

we discuss global namespace more

For now there are two things to know
1. Identifiers Declared inside the global scope are in scope from the point of declaration to the end of fle
2. Although varaibles can be defined in the global namespace this should generally be avoided.

#include <iostream> // imports the declaration of std::cout into the global scope

// All of the following statements are part of the global namespace

void foo();    // okay: function forward declaration
int x;         // compiles but strongly discouraged: uninitialized variable definition
int y { 5 };   // compiles but strongly discouraged: non-const variable definition with initializer
x = 5;         // compile error: executable statements are not allowed in namespaces

int main()     // okay: function definition
{
    return 0;
}

void goo();    // okay: A function forward declaration

All of the above are in global namespace

The std namespace

When C++ was orignally designed, all of the identifiers in the C++ standard library (including std::cin, and std::cout) were available to use without the std:: prefix (they were part of the global namespace). However this meant that any identifier in the standard library could potentially conflict with any name you picked for your own identifiers defined in the global namespace. Code that was working might suddenly have a naming conflict when you #included a new file from the standard library. Or worse, programs that would compile under one version of C++ might not compile under a new version of C++, As new identifiers introduced into the standard library could have a naming conflict with already written code. So C++ moved all of the functionality in the standard library into a namespace named std short for standard.

It turned out std::cout name isnt realy std::cout it is just cout and std is the name of the namespace that identifier cout is apart of. Because cout is defined in the std namespace, the name cout wont conflict with any objects or functions named cout that we create in the global namespace.

When accessing an identifier that is defined in a namespace (e.g std::cout) you need to tell the compiler that we are looking for a identifier defined inside the namespace (std)

When you use an identifier that is defined inside a namespace such as the std namespace you have to tell the compiler that the identifier lives inside the namespace there are a few different ways to do this.

1. Explicit Namespace qualifier std::
2. the must straightforward way to tell the compiler that we want to use cout from the std namespace is by using the std:: prefix. for example
std::cout << "Hello world";

The :: symbol  is an operator called the scope resolution operator. The identifier to the left of the :: symbol identifies the namespace, and that name to the right of :: symbol tells what identifier to look for. If no identifier is to the left of the :: symbol is provided it will assume the global namespace. 


This is the safest way to use cout because there is no ambiguity about which cout we are referencing

Best practice is to use explicit namespace prefixes to access identifiers defined in a namespace.

When an identifier includes a namespace prefix, the identifier is called  a qualified name.


2. Using namespace std (and why to avoid it)

Another way to access identifiers inside a namespace is to use a using-directive statement. Heres our orignal Hello world program with a using directive.

#include <iostream>

using namespace std; // this is a using-directive that allows us to access names in the std namespace with no namespace prefix

int main()
{
    cout << "Hello world!";
    return 0;
}


A using directive allows us to access the names in a namespace without using a namespace prefix. So in the above example, when the compiler goes to determine what the identifier cout is it will match with std::cout which, because of the using directive is accessible as just cout.

Many text, tutorials, even some IDES recommend using a using-directive at the top of this program. However used this way Is HORRIBLE practice. Consider the following program

#include <iostream> // imports the declaration of std::cout into the global scope

using namespace std; // makes std::cout accessible as "cout"

int cout() // defines our own "cout" function in the global namespace
{
    return 5;
}

int main()
{
    cout << "Hello, world!"; // Compile error!  Which cout do we want here?  The one in the std namespace or the one we defined above?

    return 0;
}

The above program doesnt compile, because the compiler now cant tell whether we want the cout function that WE defined or std::cout.

When using a using-directive in this manner, any identifier we define may conflict with ANY identically named identifier in the std namespace. Even worse while an identfier name may not conflict today with a new updates and identifiers added to the std library may cause your program to work one day and not work in the future.

Warning: Avoid using-directive such as using namespace std; at the top of program files they violate the reasons why namespaces was added in the first

3. Curly braces and indented code BTW BRACES ARE {} 

In C++, curly braces are often used to describe a scope region that is nested within another scope region (braces are also used for some non-scope related purposes, such as list initialization) for example a function defined inside the global scope region uses curly braces to separate the scope region of the function from the global scope 

In certain cases, identifier defined outside the curly braces may still be a part of the scope defined by the curly braces rather than the surrounding scope -- function parameters are a good example of this.

For example: 

#include <iostream> // imports the declaration of std::cout into the global scope

int foo(int x) // foo is defined in the global scope, x is defined within scope of foo()
{ // braces used to delineate nested scope region for function foo()
    std::cout << x << '\n';
} // x goes out of scope here

int main()
{ // braces used to delineate nested scope region for function main() 
    foo(5);

    int x { 6 }; // x is defined within the scope of main()
    std::cout << x << '\n';

    return 0;
} // x goes out of scope here
// foo and main (and std::cout) go out of scope here (the end of the file)

The code that exists inside a nested scope region is conventionally indented one level, both for readability and to help indicate that it exists inside a separate scope region. 

The #include and function definitions for foo() and main() exist in the global scope region so they are not indented. The statements inside the function exist inside the nested scope region of the function so they are indented one level