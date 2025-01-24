

How overloaded functions are differentiated

  

|Function property|Used for differentiation|Notes|
|---|---|---|
|Number of parameters|Yes||
|Type of parameters|Yes|Excludes typedefs, type aliases, and const qualifier on value parameters. Includes ellipses.|
|Return type|No|
Note that a function’s return type is not used to differentiate overloaded functions. We’ll discuss this more in a bit.


Because type aliases (or typedefs) are not distinct types, overloaded functions using type aliases are not distinct from overloads using the aliased type. For example, all of the following overloads are not differentiated (and will result in a compile error):

```cpp
typedef int Height; // typedef
using Age = int; // type alias

void print(int value);
void print(Age value); // not differentiated from print(int)
void print(Height value); // not differentiated from print(int)
```


The return type of a function is not considered for differentiation

A function’s return type is not considered when differentiating overloaded functions.

Consider the case where you want to write a function that returns a random number, but you need a version that will return an int, and another version that will return a double. You might be tempted to do this:

```cpp
int getRandomValue();
double getRandomValue();
```

Copy

On Visual Studio 2019, this results in the following compiler error:

error C2556: 'double getRandomValue(void)': overloaded function differs only by return type from 'int getRandomValue(void)'

This makes sense. If you were the compiler, and you saw this statement:

```cpp
getRandomValue();
```

Copy

Which of the two overloaded functions would you call? It’s not clear.
Type signature

A function’s **type signature** (generally called a **signature**) is defined as the parts of the function header that are used for differentiation of the function. In C++, this includes the function name, number of parameters, parameter type, and function-level qualifiers. It notably does _not_ include the return type.


