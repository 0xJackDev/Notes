

Go only has one loop. the for loop. It can act as both the traditional C++ for loop as well as be a "while" loop


## IF with a short statement

like *for*, the *if* statement can start with a short statement to execute before the condition. 

Variables declared by the statement are only in scope until the end of the if statement

```
if v := math.Pow(x, n); v < lim {
		return v
	} // V is destroyed as the IF statement is over
```



## IF and else

Variables declared inside an if short statement are also available inside of the ELSE blocks

```
	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g\n", v, lim)
	}
	// can't use v here, though
	return lim
```



## Exercise: Loops and functions

Computers typically compute the square root of x using a loop. Starting with some guess z, we can adjust z based on how close z² is to x, producing a better guess:

z -= (z*z - x) / (2*z)

Lets calculate this 10 times and return the closest z sqrt 

```
func Sqrt(x float64) float64 {
	z := 1.0
	for i := 0; i < 10; i++{
		z -= (z*z - x) / (2*z)		
	}
	return z;
	
}
```




## Switch

Heres how you do a switch statement in go


```
switch os := runtime.GOOS; os{
case "darwin":
	fmt.Println("MACOS")
case "linix":
	fmt.Println("Linux")

default:

	
}
```



Switch cases evaluate cases from top to bottom and will stop when a case successedes. 




## Switch with no condition

Switch without a condition is the same as switch true. 


This construct can be clean to write compared to long if-else chains


```
	switch {
	case t.Hour() < 12:
		fmt.Println("Good morning!")
	case t.Hour() < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}
```




## Defer

A defer statement defers the execution of a function until the surruonding function returns.

A deferred calls arguments are evaluated immediately but the function call is not executed until the surrounding function returns.

```
func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}
```

For example this prints hello world as the deferred function only prints when the MAIN function is done running. 

Deferred functions are pushed onto a stack. When a function returns its deferred calls are executed in last-in-first-out order.

https://go.dev/blog/defer-panic-and-recover



