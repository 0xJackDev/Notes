


When you make a semantic error, that error may or may not be immediately noticeable when you run your program. An issue may lurk undetected in your code for a long time before newly introduced code or changed circumstances cause it to manifest as a program malfunction. The longer an error sits in the code base before it is found, the more likely it is to be hard to find, and something that may have been easy to fix originally turns into a debugging adventure that eats up time and energy. 

As you add new capabilities to your programs (“behavioral changes”), you will find that some of your functions grow in length. As functions get longer, they get both more complex and harder to understand.

One way to address this is to break a single long function into multiple shorter functions. This process of making structural changes to your code without changing its behavior is called **refactoring**. The goal of refactoring is to make your program less complex by increasing its organization and modularity.


Errors can be not only of your own making (e.g. incorrect logic), but also occur when your users use the application in a way that you did not anticipate. For example, if you ask the user to enter an integer, and they enter a letter instead, how does your program behave in such a case? Unless you anticipated this, and added some error handling for this case, probably not very well.



Defensive programming is a practice whereby the programmer tries to anticipate all of the ways the software can bemisued. 



An introduction to testing functions

One common way to help uncover issues with your program is to write testing functions to “exercise” the code you’ve written. Here’s a primitive attempt, more for illustrative purposes than anything:

```cpp
#include <iostream>

int add(int x, int y)
{
	return x + y;
}

void testadd()
{
	std::cout << "This function should print: 2 0 0 -2\n";
	std::cout << add(1, 1) << ' ';
	std::cout << add(-1, 1) << ' ';
	std::cout << add(1, -1) << ' ';
	std::cout << add(-1, -1) << ' ';
}

int main()
{
	testadd();

	return 0;
}
```


The testadd() function tests the add() function by calling it with different values. If all the values match our expectations, then we can be reasonably confident the function works. Even better, we can keep this function around, and run it any time we change function _add_ to ensure we haven’t accidentally broken it.




[Many static analysis tools exist](https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis#C,_C++), some of which can identify over 300 types of programming errors. On our small academic programs, use of a static analysis tool is optional, but using one may help you find areas where your code is non-compliant with best practices. On large programs, use of a static analysis tool is highly recommended, as it can surface tens or hundreds of potential issues.


Use a static analysis tool on your programs to help find areas where your code is non-compliant with best practices.