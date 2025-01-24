# 8.14 — Generating random numbers using Mersenne Twister

[_Alex_](https://www.learncpp.com/author/Alex/ "View all posts by Alex")  May 8, 2024

In the previous lesson [8.13 -- Introduction to random number generation](https://www.learncpp.com/cpp-tutorial/introduction-to-random-number-generation/), we introduced the concept of random number generation, and discussed how PRNG algorithms are typically used to simulate randomness in programs.

In this lesson, we’ll take a look at how to generate random numbers in your programs. To access any of the randomization capabilities in C++, we include the `<random>` header of the standard library.


Generating random numbers in C++ using Mersenne Twister

The Mersenne Twister PRNG, besides having a great name, is probably the most popular PRNG across all programming languages. Although it is a bit old by today’s standards, it generally produces quality results and has decent performance. The random library has support for two Mersenne Twister types:

- `mt19937` is a Mersenne Twister that generates 32-bit unsigned integers
- `mt19937_64` is a Mersenne Twister that generates 64-bit unsigned integers

Using Mersenne Twister is straightforward:

```cpp
#include <iostream>
#include <random> // for std::mt19937

int main()
{
	std::mt19937 mt{}; // Instantiate a 32-bit Mersenne Twister

	// Print a bunch of random numbers
	for (int count{ 1 }; count <= 40; ++count)
	{
		std::cout << mt() << '\t'; // generate a random number

		// If we've printed 5 numbers, start a new row
		if (count % 5 == 0)
			std::cout << '\n';
	}

	return 0;
}
```


or just 

```
#include <iostream>
#include <random>


int main() {
	std::mt19937_64 ranNum{};

	std::cout << ranNum();
}
```

will generate one random 64 bit number


Rolling a dice using Mersenne Twister

A 32-bit PRNG will generate random numbers between 0 and 4,294,967,295, but we do not always want numbers in that range. If our program was simulating a board game or a dice game, we’d probably want to simulate the roll of a 6-sided dice by generating random numbers between 1 and 6. If our program was a dungeon adventure, and the player had a sword that did between 7 and 11 damage to monsters, then we’d want to generate random numbers between 7 and 11 whenever the player hit a monster.

Unfortunately, PRNGs can’t do this. They can only generate numbers that use the full range. What we need is some way to convert a number that is output from our PRNG into a value in the smaller range we want (with an even probability of each value occurring). While we could write a function to do this ourselves, doing so in a way that produces non-biased results is non-trivial.

Fortunately, the random library can help us here, in the form of random number distributions. A **random number distribution** converts the output of a PRNG into some other distribution of numbers.

As an aside…

For the stats geeks: a random number distribution is just a probability distribution designed to take PRNG values as input.

The random library has many random numbers distributions, most of which you will never use unless you’re doing some kind of statistical analysis. But there’s one random number distribution that’s extremely useful: a **uniform distribution** is a random number distribution that produces outputs between two numbers X and Y (inclusive) with equal probability.

Here’s a similar program to the one above, using a uniform distribution to simulate the roll of a 6-sided dice:

```cpp
#include <iostream>
#include <random> // for std::mt19937 and std::uniform_int_distribution

int main()
{
	std::mt19937 mt{};

	// Create a reusable random number generator that generates uniform numbers between 1 and 6
	std::uniform_int_distribution die6{ 1, 6 }; // for C++14, use std::uniform_int_distribution<> die6{ 1, 6 };

	// Print a bunch of random numbers
	for (int count{ 1 }; count <= 40; ++count)
	{
		std::cout << die6(mt) << '\t'; // generate a roll of the die here

		// If we've printed 10 numbers, start a new row
		if (count % 10 == 0)
			std::cout << '\n';
	}

	return 0;
}
```

Copy

This produces the result:

3       1       3       6       5       2       6       6       1       2
2       6       1       1       6       1       4       5       2       5
6       2       6       2       1       3       5       4       5       6
1       4       2       3       1       2       2       6       2       1

There are only two noteworthy differences in this example compared to the previous one. First, we’ve created a uniform distribution variable (named `die6`) to generate numbers between 1 and 6. Second, instead of calling `mt()` to generate 32-bit unsigned integer random numbers, we’re now calling `die6(mt)` to generate a value between 1 and 6.


To generate a random number between one and a hundred. 

```
#include <iostream>
#include <random>


int main() {
	std::mt19937_64 ranNum{};


	std::uniform_int_distribution Hunnid(1, 100);


	std::cout << Hunnid(ranNum);
}
```


The above program isn’t as random as it seems we need to add a random seed value that changes so its different every time we run our program otherwise it will be the same because the way that the MT algorithm works is predetermistic. so we initalize this with a seed which is our Systems time clock that is why we add the chrono header. The annoying part here is we type cast the result type. then we use the (std::chrono::steady_clock::now().time_since_epoch().count())}; for the value we are looking for. 




```
#include <iostream>
#include <random>
#include <chrono>

int main() {
	std::mt19937_64 ranNum{ static_cast<std::mt19937_64::result_type>(std::chrono::steady_clock::now().time_since_epoch().count())};


	std::uniform_int_distribution Hunnid(1, 100);


	std::cout << Hunnid(ranNum);
}
```

read below to understand more

A way easier way to do this is by using the std::random_device{}() method thats inside of the random library so to generate a number between 1 and 100 use. This is alot more readable to me so.
```

#include <iostream>
#include <random>

int main() {
	std::mt19937_64 ranNum{ std::random_device{}() };


	std::uniform_int_distribution Hunnid(1, 100);


	std::cout << Hunnid(ranNum);
}
```


Although the results of our dice rolling example above are pretty random, there’s a major flaw with the program. Run the program 3 times and see if you can figure out what it is. Go ahead, we’ll wait.

_Jeopardy music_

If you run the program multiple times, you will note that it prints the same numbers every time! While each number in the sequence is random with regards to the previous one, the entire sequence is not random at all! Each run of our program produces the exact same result.



Imagine that you’re writing a game of hi-lo, where the user has 10 tries to guess a number that has been picked randomly, and the computer tells the user whether their guess is too high or too low. If the computer picks the same random number every time, the game won’t be interesting past the first time it is played. So let’s take a deeper look at why this is happening, and how we can fix it.

In the prior lesson ([8.13 -- Introduction to random number generation](https://www.learncpp.com/cpp-tutorial/introduction-to-random-number-generation/)), we covered that each number in a PRNG sequence is in a deterministic way. And that the state of the PRNG is initialized from the seed value. Thus, given any starting seed number, PRNGs will always generate the same sequence of numbers from that seed as a result.

Because we are value initializing our Mersenne Twister, it is being initialized with the same seed every time the program is run. And because the seed is the same, the random numbers being generated are also the same.

In order to make our entire sequence randomized differently each time the program is run, we need to pick a seed that’s not a fixed number. The first answer that probably comes to mind is that we need a random number for our seed! That’s a good thought, but if we need a random number to generate random numbers, then we’re in a catch-22. It turns out, we really don’t need our seed to be a random number -- we just need to pick something that changes each time the program is run. Then we can use our PRNG to generate a unique sequence of pseudo-random numbers from that seed.

There are two methods that are commonly used to do this:

- Use the system clock
- Use the system’s random device

Seeding with the system clock

What’s one thing that’s different every time you run your program? Unless you manage to run your program twice at exactly the same moment in time, the answer is that the current time is different. Therefore, if we use the current time as our seed value, then our program will produce a different set of random numbers each time it is run. C and C++ have a long history of PRNGs being seeded using the current time (using the `std::time()` function), so you will probably see this in a lot of existing code.

Fortunately, C++ has a chrono library containing various clocks that we can use to generate a seed value. To minimize the chance of two time values being identical if the program is run quickly in succession, we want to use some time measure that changes as quickly as possible. For this, we’ll ask the clock how much time has passed since the earliest time it can measure. This time is measured in “ticks”, which is a very small unit of time (usually nanoseconds, but could be milliseconds).

```cpp
#include <iostream>
#include <random> // for std::mt19937
#include <chrono> // for std::chrono

int main()
{
	// Seed our Mersenne Twister using steady_clock
	std::mt19937 mt{ static_cast<std::mt19937::result_type>(
		std::chrono::steady_clock::now().time_since_epoch().count()
		) };

	// Create a reusable random number generator that generates uniform numbers between 1 and 6
	std::uniform_int_distribution die6{ 1, 6 }; // for C++14, use std::uniform_int_distribution<> die6{ 1, 6 };

	// Print a bunch of random numbers
	for (int count{ 1 }; count <= 40; ++count)
	{
		std::cout << die6(mt) << '\t'; // generate a roll of the die here

		// If we've printed 10 numbers, start a new row
		if (count % 10 == 0)
			std::cout << '\n';
	}

	return 0;
}
```




Tip

`std::chrono::high_resolution_clock` is a popular choice instead of `std::chrono::steady_clock`. `std::chrono::high_resolution_clock` is the clock that uses the most granular unit of time, but it may use the system clock for the current time, which can be changed or rolled back by users. `std::chrono::steady_clock` may have a less granular tick time, but is the only clock with a guarantee that users cannot adjust it.



Seeding with the random device

The random library contains a type called `std::random_device` that is an implementation-defined PRNG. Normally we avoid implementation-defined capabilities because they have no guarantees about quality or portability, but this is one of the exception cases. Typically `std::random_device` will ask the OS for a pseudo-random number (how it does this depends on the OS).

```cpp
#include <iostream>
#include <random> // for std::mt19937 and std::random_device

int main()
{
	std::mt19937 mt{ std::random_device{}() };

	// Create a reusable random number generator that generates uniform numbers between 1 and 6
	std::uniform_int_distribution die6{ 1, 6 }; // for C++14, use std::uniform_int_distribution<> die6{ 1, 6 };

	// Print a bunch of random numbers
	for (int count{ 1 }; count <= 40; ++count)
	{
		std::cout << die6(mt) << '\t'; // generate a roll of the die here

		// If we've printed 10 numbers, start a new row
		if (count % 10 == 0)
			std::cout << '\n';
	}

	return 0;
}
```

Copy

In the above program, we’re seeding our Mersenne Twister with one random number generated from a temporary instance of `std::random_device`. If you run this program multiple times, it should also produce different results each time.

One potential problem with `std::random_device`: it isn’t required to be non-deterministic, meaning it _could_, on some systems, produce the same sequence every time the program is run, which is exactly what we’re trying to avoid. There was a [bug in MinGW](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=85494) (fixed in GCC 9.2) that would do exactly this, making `std::random_device` useless.

However, the latest versions of the most popular compilers (GCC/MinGW, Clang, Visual Studio) support proper implementations of `std::random_device`.

Best practice

Use `std::random_device` to seed your PRNGs (unless it’s not implemented properly for your target compiler/architecture).


Only seed a PRNG once

Many PRNGs can be reseeded after the initial seeding. This essentially re-initializes the state of the random number generator, causing it to generate results starting from the new seed state. Reseeding should generally be avoided unless you have a specific reason to do so, as it can cause the results to be less random, or not random at all.

Best practice

Only seed a given pseudo-random number generator once, and do not reseed it.


Here’s an example of a common mistake that new programmers make:

```cpp
#include <iostream>
#include <random>

int getCard()
{
    std::mt19937 mt{ std::random_device{}() }; // this gets created and seeded every time the function is called
    std::uniform_int_distribution card{ 1, 52 };
    return card(mt);
}

int main()
{
    std::cout << getCard() << '\n';

    return 0;
}
```

Copy

In the `getCard()` function, the random number generator is being created and seeded every time the function is called. This is inefficient at best, and will likely cause poor random results.


so to fix that make the std::mt19937 static. 