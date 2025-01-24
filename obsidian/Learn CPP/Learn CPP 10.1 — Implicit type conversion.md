
Introduction to type conversion

The value of an object is stored as a sequence of bits, and the data type of the object tells the compiler how to interpret those bits into meaningful values. Different data types may represent the “same” number differently. For example, the integer value `3` might be stored as binary `0000 0000 0000 0000 0000 0000 0000 0011`, whereas floating point value `3.0` might be stored as binary `0100 0000 0100 0000 0000 0000 0000 0000`.

So what happens when we do something like this?

```cpp
float f{ 3 }; // initialize floating point variable with int 3
```

Copy

In such a case, the compiler can’t just copy the bits representing the `int` value `3` into the memory allocated for `float` variable `f`. Instead, it needs to convert the integer value `3` to the equivalent floating point value `3.0`, which can then be stored in the memory allocated for `f`.

The process of producing a new value of some type from a value of a different type is called a **conversion**.



Type conversion can be invoked in one of two ways: either implicitly (as needed by the compiler), or explicitly (when requested by the programmer). We’ll cover implicit type conversion in this lesson, and explicit type conversions (casting) in upcoming lesson [10.6 -- Explicit type conversion (casting) and static_cast](https://www.learncpp.com/cpp-tutorial/explicit-type-conversion-casting-and-static-cast/).




Implicit type conversion

**Implicit type conversion** (also called **automatic type conversion** or **coercion**) is performed automatically by the compiler when one data type is required, but a different data type is supplied. The vast majority of type conversions in C++ are implicit type conversions. For example, implicit type conversion happens in all of the following cases:

When initializing (or assigning a value to) a variable with a value of a different data type:

```cpp
double d{ 3 }; // int value 3 implicitly converted to type double
d = 6; // int value 6 implicitly converted to type double
```

Copy

When the type of a return value is different from the function’s declared return type:

```cpp
float doSomething()
{
    return 3.0; // double value 3.0 implicitly converted to type float
}
```

Copy

When using certain binary operators with operands of different types:

```cpp
double division{ 4.0 / 3 }; // int value 3 implicitly converted to type double
```

Copy

When using a non-Boolean value in an if-statement:

```cpp
if (5) // int value 5 implicitly converted to type bool
{
}
```

Copy

When an argument passed to a function is a different type than the function parameter:

```cpp
void doSomething(long l)
{
}

doSomething(3); // int value 3 implicitly converted to type long
```




What happens when a type conversion is invoked

When a type conversion is invoked (whether implicitly or explicitly), the compiler will determine whether it can convert the value from the current type to the desired type. If a valid conversion can be found, then the compiler will produce a new value of the desired type. Note that type conversions don’t change the value or type of the value or object being converted.

If the compiler can’t find an acceptable conversion, then the compilation will fail with a compile error. Type conversions can fail for any number of reasons. For example, the compiler might not know how to convert a value between the original type and the desired type. In other cases, statements may disallow certain types of conversions. For example:

```cpp
int x { 3.5 }; // brace-initialization disallows conversions that result in data loss
```

Copy

Even though the compiler knows how to convert a `double` value to an `int` value, such conversions are disallowed when using brace-initialization.

There are also cases where the compiler may not be able to figure out which of several possible type conversions is unambiguously the best one to use. We’ll see examples of this in lesson [11.3 -- Function overload resolution and ambiguous matches](https://www.learncpp.com/cpp-tutorial/function-overload-resolution-and-ambiguous-matches/).

So how does the compiler actually determine whether it can convert a value from one type to another?

The standard conversions

The C++ language standard defines how different fundamental types (and in some cases, compound types) can be converted to other types. These conversion rules are called the **standard conversions**.

The standard conversions can be broadly divided into 4 categories, each covering different types of conversions:

- Numeric promotions (covered in lesson [10.2 -- Floating-point and integral promotion](https://www.learncpp.com/cpp-tutorial/floating-point-and-integral-promotion/))
- Numeric conversions (covered in lesson [10.3 -- Numeric conversions](https://www.learncpp.com/cpp-tutorial/numeric-conversions/))
- Arithmetic conversions (covered in lesson [10.5 -- Arithmetic conversions](https://www.learncpp.com/cpp-tutorial/arithmetic-conversions/))
- Other conversions (which includes various pointer and reference conversions)

When a type conversion is needed, the compiler will see if there are standard conversions that it can use to convert the value to the desired type. The compiler may apply zero, one, or (in certain cases) two standard conversions in the conversion process.




