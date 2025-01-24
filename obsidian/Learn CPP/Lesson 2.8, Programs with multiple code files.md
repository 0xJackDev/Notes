AS programs get larger, its common to split them into multiple files. One advantage of working with an IDE is that it makes this alot easier


The compiler compiles each file individually. It does not know about the content of other code files, or remember anything it has seen from previously compiled code files. SO even though the compiler may has seen the definition of the function add previously if it compiled add.cpp fire it doesn't remember. This limited visibility and short memory is intentional.

it allows the source files of a project to be compiled in any order
when we change a source file only that source file needs to be recompiled
It reduces the possibility of naming conflicts between identifiers in different files.

We will explore what happens when names do conflict 

In order to use a function made in other source file you must do the same thing as if it was under the main function, you must use a declaration before main. Now if you add a declaration it will know what identifier to be satisfied and the linker will connect the function call to add in main.cpp

Using this method we can give files access to functions that live in another file

Because the compiler compiles each code file individually (and forgets what its seen), each code file that uses std::cout or std::cin needs to #include iostream 

When an identifier is used in an expression, the identifier must be connected to its definition (remember identifier is a functions name and parameters)

There are plently of things that can go wrong the first time you try to work with multiple files. If you tried the aboce example and ran into an error you should try the following.

1. If you get a compile error about add not being defined in main, you proably forgot the forward declaration for add in the main.cpp file
2. If you get a linker error about add not being defined like unresolved external symbol "int __cdecl add(int,int)" (?add@@YAHHH@Z) referenced in function _main. The most likely reason is that add.cpp isnt added to your project correctly. And when you compile you should see the compiler list both main.cpp and add.cpp if you see main.cpp and add.cpp isnt getting compiled you should see add.cpp listed in the solution explorer, if you dont right click your project and add the file and try compiler again. But there is other reasons this can happen, like for example if you added add.cpp to the wrong project or that file is not set to compile or link in visual stuidos settings
3. Do not #include "add.cpp" from main.cpp this will cause the preproccesor to insert the contents of add.cpp into main.cpp instead of treating them as different files


C++ is designed so that each source file can be compiled indepentitly with no knowledge of what is in other files. Therefore the order in which are compiled should not be relevant

We will begin working with multiple files alot when we get into object oritented programming

Whenever you create a new .cpp file you need to add it to your project so it getsc ompiled