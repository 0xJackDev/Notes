


## Packages

Every Go program is made up of packages. 

Programs start running in package main.

This program below is using the packages with import paths "fmt" and "math/rand"

By convention the package name is the same as the last element of the import path. For instance, the math/rand package compromises files that begin with the statement package rand.


```
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite number is", rand.Intn(10))
}

```


This code groups the imports into a parenthesized, "factored" import statement.

You can also write multiple import statements, like:

import "fmt"
import "math"

But it is good style to use the factored import statement.




## Exported names

In Go, a name is exported if it begins with a capital letter. For example, Pizza is an exported name as is Pi, which is exported from the math package.

Pizza and Pi do not start with a capital letter so they are not exported.


When importing a package you can only refer to it by its exported names. Any "unexported" names are not accessible from outside the package. For example if you use math.pi instead of math.Pi it will cause an error. 

Exported names are always started with capital




## Functions

declare a function with the func keyword

A function can take zero or more arguments.

NOW this is where GO is different then any other programming language ive used. The type comes after the variables name as well as the type of function comes after the parameters. For example

```
func add(x int, y int) int {
	return x + y
}
```

This is because GO is different then C syntax to understand why GO does this read here

https://go.dev/blog/declaration-syntax

but basically its just to be easier to read once shit gets complex w pointers.


When two or more consecutive named function parameters share a type you can omit a type from all but the last. AKA if all your function parameters are type int instead of type x int, y int you can just type *(x, y int) * 




## Multiple Results 

A function can return any number of results. For example this Swap function returns two strings in opposite order of which you called it.


```
func swap(x, y string) (string, string) {
	return y, x
}
```


## named Return Values

Go's return values may also be named. If so they are treated as variables defined at the top of a function.

These names should be used to document the meaning of the return values.

A return statement without arguments returns the named return values. AKA a "naked" return.

Naked return statements should only be used in short functions and can harm readability in longer functions 

```
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	fmt.Println(split(17))
}

```

This program would like 7 10

Since BOTH return values are returned to fmt.Println() they are both logged to screen.




## Variables 
You must use the var keyword to declare and initialize variable unless using the := operator


the *var* statement declares a list of variables; as in function argument lists the type is last.

A var statement can be at the package or function level. we see both in this example.

```
package main

import "fmt"

var c, python, java bool # Declares three variables with a type of bool

func main() {
	var i int # Declares variable i with the type of int
	fmt.Println(i, c, python, java)
}

```



## Variables with initializers.

A var declaration can include initializers, one per variable

If an initializer is present, the type can be omitted; the variable will take the type of the initializer

```
package main

import "fmt"

var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}

```

This prints

1 2 true false no!




## Short variable declarations

inside of a function, the := short assignment statement can be used in place of a var declaration 

```
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	eee := 3
	k := 3
	c, python, java := true, false, "no!"

	fmt.Println(i, j, k, c, python, java, eee)
}

```

for example.





## Go's Basic Types
Go's basic types are

```
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128

```
The example shows variables of several types, and also that variable declarations may be "factored" into blocks, as with import statements.

The `int`, `uint`, and `uintptr` types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems. When you need an integer value you should use `int` unless you have a specific reason to use a sized or unsigned integer type.




## Zero values

Variables that are declared without an explicit initial value are given their zero value.


The zero value is:
	0 for numeric types
	false for boolean type and
	" " (empty strings) for strings





## Type conversions

the expression *T(v)* converts value v to the type of T

for example


```
Some numeric conversions:

var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

Or, put more simply:

i := 42
f := float64(i)
u := uint(f)
```


Unlike in C, In GO assignment between items of different types require explicit conversion.




## Type inference

When declaring a variable without a explicit type (either by using :=  syntax or var = syntax) The variables type is inferred from the value on the right hand sight.

When the right hand side of the declaration is typed, the new variable is of that same type:

```
var i int
j := i // j is an int

```
But when the right hand side contains an untyped numeric constant, the new variable may be an `int`, `float64`, or `complex128` depending on the precision of the constant:

```
i := 42           // int
f := 3.142        // float64
g := 0.867 + 0.5i // complex128


```


```

func main() {
	v := 42.555555 // change me!
	fmt.Printf("v is of type %T\n", v)
}
```

in this case v is a float64




## Constants
Constants are declared like variables, but with the const keyword instead of var.

Constants can be character, string, boolean or numeric values.

Constants CANNOT be declared using the := syntax


```
const Pi = 3.14

Declares a const variable named Pi to be a float
```


## Numeric Constans


Numeric constants are high-precision values. 

An untyped constant takes the type needed by its contaxt.

Try printing needInt(Big) too

```
package main

import "fmt"

const (
	// Create a huge number by shifting a 1 bit left 100 places.
	// In other words, the binary number that is 1 followed by 100 zeroes.
	Big = 1 << 100
	// Shift it right again 99 places, so we end up with 1<<1, or 2.
	Small = Big >> 99
)

func needInt(x int) int { return x*10 + 1 }
func needFloat(x float64) float64 {
	return x * 0.1
}

func main() {
	fmt.Println(needInt(Small))
	fmt.Println(needFloat(Small))
	fmt.Println(needFloat(Big))
	fmt.Println(needInt(Small))
}
```



## For Loops

Go has only one looping construct, the for loop/

The basic for loop has three components separated by semicolons: 
 the init statement: executed before the first iteration
 ;
the condition expression: evaluated before every iteration
;
the post statement: executed at the end of every iteration
{

}

The init statement will often be a short variable declaration, and the variables declared there are visible only in the scope of the `for` statement.

**Note:** Unlike other languages like C, Java, or JavaScript there are no parentheses surrounding the three components of the `for` statement and the braces `{ }` are always required.


```
package main

import "fmt"

func main() {
	sum := 0
	
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}

```


The init and post statements are optional.

```
package main

import "fmt"

func main() {
	sum := 1
	for ; sum < 1000; {
		sum += sum
	}
	fmt.Println(sum)
}

```


For is Go's "while"


```
package main

import "fmt"

func main() {
	sum := 1
	for sum < 1000 {
		sum += sum
	}
	fmt.Println(sum)
}

```

## Forever

If you omit the loop condition it loops forever, so an infinite loop is compactly expressed.


```
package main

func main() {
	for {
	}
}

```



## If

Go's IF statements are like its *for* loops; the expression does not need to be surronded by parentheses ( ) but the braces are required { }

```
func sqrt(x float64) string {
	if x < 0 {
		return sqrt(-x) + "i"
	}
	return fmt.Sprint(math.Sqrt(x))
}

```

