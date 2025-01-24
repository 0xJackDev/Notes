
The rest of my notes are in LearnCPP.txt Before this I will be using obsidian from now on.

Take a look at this seemingly innocent program 

#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';
    return 0;
}

int add(int x, int y)
{
    return x + y;
}


You expect this program to output 7 but instead we get a compile error that the identifier add 

This is because the compiler compiles the contents of the code files sequentially (top to bottom). When the compiler reaches the function call to add on line 5 of main, it doesnt know what add is because we haven't defined add until line 9! that produces the error, Identifier not found.

*its Fairly common for a single error to produce many redundant or related errors or warnings. it can sometimes be hard to tell whether any error beyond the first is a consequence of the first issue or an independent issue on its own*

When addressing compilation errors or warnings in your programs, resolve the first issue listed and then compile again.
To fix this problem, we need to address the fact that the compiler doesnt know what add is there are two common ways to address the issue.

Option 1: Reorder the function definitions

#include <iostream>

int add(int x, int y)
{
    return x + y;
}

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';
    return 0;
}

Simply Moving the add function above main will work as it defines the function before its first call, In a larger program it can be tedious trying to figure out which functions call to other functions and in what order they should be declared.

Furthermore this option is not always possible. Lets say we are writing a program that has two functions A and B. If function A calls to function B and function B calls function A theres no correct w ay to order the functions to make the compiler happy. 

Option 2: use Forward declaration

We can also fix this by using a forward declaration.

A forward declaration allows us to tell the compiler about the existence of a function identifier before actually defining the identifier.

In the case of functions this allows us to tell the compiler about the existence of a function before we define the functions body. This way when the compiler encounters a call to the function, It will understand we are making a function call and can check to make sure we are calling the function correctly even if t doesn't yet know how or where the function is defined, This is A Declaration. And a forward declaration in this case.

To write a forward declaration for a function we use a function declaration statement (also called a function prototype). the function declaration consists of the functions return type, name, and parameter types terminatedwith a semicolon. The names of the parameters can be optionally included. The function body is not included

For example here is a function declaration for the add function:

int add(int x, int y);

And heres our orignal program which didnt compile using a forward declaration

#include <iostream>

int add(int x, int y); // forward declaration of add() (using a function declaration)

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n'; // this works because we forward declared add() above
    return 0;
}

int add(int x, int y) // even though the body of add() isn't defined until here
{
    return x + y;
}

When the compiler reaches the call o add in main, it will need to know what the add function does and looks like ( a function that takes two int parameters and returns a integer) and it wont complain

It is worth noting that function declaration do not need to specify the names of the parameters (as they are not considered to be part of a functions declaration). In the above code, you can also forward your function like this
int add(int, int);

However we prefer to name our parameters as it will help us understand what it does just by looking at it

Also many automated generation tools will generate documentation from the content header files, which is where declarations are often placed.

*best practice is to name the parameters in your function declarations*

You can easily create function declarations by pasting your functions header and adding a semicolon


Why forward declarations.

You may wonder why to use a forward declaration instead of re format. well there are multiple reasons

Most often, forward declarations are used to tell the compiler about the existence of some function that has been defined in a different code file. Reordering isn't possible in this scenario because the caller and callee are in completely different files.

Forward declarations can also be used to define our functions in an order-agnostic manner. This allows us to define functions in whatever order maximizes organization (e.g. by clustering related functions together)

Less often there are times when two functions call each other.


Forgetting the function body 

New programmers often wonder what happens if they forward a function but do not define it

The answer s it depends. If a forward declaration is made but the function is never called the program will run and compile fine but if the forward declaration is made and the function is called but the program never defines the function the program will compile okay but we will get a linker error as the function can resolve the function call.

Other types of forward declaratiosn

In C++ you will often hear the words declaration and definition used, 

A declaration tells the compiler about the existence of a identifier and its associated type  information. Here are some examples of declarations Example:
int add(int x, int y); // tells the compiler about a function named "add" that takes two int parameters and returns an int.  No body!
int x;                 // tells the compiler about an integer variable named x

A definition is a declaration that has a body and actually implements (for functions or types) or instantiates the variables Example:
int add(int x, int y) // implements function add()
{
    int z{ x + y };   // instantiates variable z

    return z;
}

int x;                // instantiates variable x

In C++ all definitions are also declarations therefor int x; is both a definition and declaration

Conversely not all declarations are Definitions. Declarations that arent definitions are called pure declarations. Types of pure declarations include forward declarations for function, variables, and types

When the compiler encounters an identifier it will check to ensure that the identifier is valid, (e.g that the identifier is in scope and in syntactically valid)

In most cases, a declaration is sufficient to allow the compiler to ensure an identifier is being used properly. For excample when the compiler encounters function call. add(5,6) it has already seen the declaration add(int,int) then can validate that add is actually a function and takes two int parameter it does not need to actually have seen the definition for add which may exist in another file

However there are a few cases where the compiler must be able to see a full definition in order ot use an identifier (such as for template and type definitions)

Declaration                 Tells compiler about an identifier and its associated type information.      void foo(); // function forward declaration (no body)  
void goo() {}; // function definition (has body)  
int x; // variable definition


Definition        Implements a function or instantiates a variable. Definitions are also declarations.     
Definitions are also declarations. void foo() { } // function definition (has body)  int x; // variable definition

|Pure declaration|                 A declaration that isn’t a definition.             
void foo(); // function forward declaration (no body)


Initialization                Provides an initial value for a defined object.      |
|int x { 2 }; // 2 is the initializer|          


The one definition rule (ODR)

the one definition rule (or ODR for short) is a well known rule in C++. The ODR has 3 parts:
1. Within a file, each function, variable, type, or template can o not have one definition. Definitions occurring in different scopes that cannot see each other do not violate  this rule.
2. Within a program each function or variable can only have one definition. This rule exists because programs can have more than one file. Functions and variables not visible to the linker are excluded from this rule
3. Types, templates, inline functions, and inline variables are allows to have duplicate definitions in different files, so long as each definition is identical. We haven't covered what most of these things are yet so don't worry about this for now 


Violating part 1 of the ODR will cause the compiler to issue a redefinition error. Violation ODR part 2 will cause the linker to issue a redefinition error.  Violating ODR part three will result in undefined behavior 

int add(int x, int y)
{
     return x + y;
}

int add(int x, int y) // violation of ODR, we've already defined function add(int, int)
{
     return x + y;
}

int main()
{
    int x{};
    int x{ 5 }; // violation of ODR, we've already defined x
}


In this example function add(int,int) is defined twice in the global scope, and local variable int x is defined twice in the scope of main().
However its not a violation of ODR part 1 for main() to have a local variable defined as int x and add() to have a different function parameter as defined in int x. These definitions occur in different scopes.

Functions that share an identifier but have a different set of parameters are also considered to be their own separate functions and do NOT violate ODR

A function prototype is a declaration statement that includes the functions name, return type, parameter types, and optionally the parameter names. It does not include the function body and tells the compiler about the existence of a function before it is defined.

A forward declaration tells the compiler that an identifier exists before it is actually defined.

For functions, a function declaration/prototype serves as a forward declaration.