

Scientific Notation is a useful shorthand for writing lengthy numbers in a concise manner. And although scientific notation may seem foreign at first, understanding it will help you understand how floating point numbers work, and more importantly what their limitations are.


Numbers in scientific notation take the following form: *significand* x 10^exponent
For example in the scientific notation 1.2 x 10^4
1.2 is the significand and 4 is the exponent and since 10 to the fourth power evaluates to 10,000 the equation above evaluates to 12,000 


By convention, numbers in scientific notation are written with one digit before the decimal point, and the rest of the digits afterward.

Consider the mass of the Earth. In decimal notation, we’d write this as `5972200000000000000000000 kg`. That’s a really large number (too big to fit even in an 8 byte integer). It’s also hard to read (is that 19 or 20 zeros?). Even with separators (5,972,200,000,000,000,000,000,000) the number is still hard to read.


In scientific notation, this would be written as `5.9722 x 10²⁴ kg`, which is much easier to read. Scientific notation has the added benefit of making it easier to compare the magnitude of two extremely large or small numbers simply by comparing the exponent.


Because it can be hard to type or display exponents in C++, we use the letter ‘e’ (or sometimes ‘E’) to represent the “times 10 to the power of” part of the equation. For example, `1.2 x 10⁴` would be written as `1.2e4`, and `5.9722 x 10²⁴` would be written as `5.9722e24`.


For numbers smaller than 1, the exponent can be negative. The number `5e-2` is equivalent to `5 * 10⁻²`, which is `5 / 10²`, or `0.05`. The mass of an electron is `9.1093837e-31 kg`.



## Significant digits


Let’s say you need to know the value of the mathematical constant pi for some equation, but you’ve forgotten. You ask two people. One tells you the value of pi is `3.14`. The other tells you the value of pi is `3.14159`. Both of these values are “correct”, but the latter is far more precise.


Heres one more important thing to understand about scientific notation: the digits in the significand (the part before the 'e' ) are called the significant digits or significant figures. The more significant digits the more precise a number is. 


In scientific notation, we’d write `3.14` as `3.14e0`. Since there are 3 numbers in the significand, this number has 3 significant digits.

`3.14159` would be written as `3.14159e0`. Since there are 6 numbers in the significand, this number has 6 significant digits.




## how to convert decimal numbers to scientific notation

Use the following procedure:

- Your exponent starts at zero
- Slide the decimal left or right so there is only one non-zero digit to the left of the decimal 
	- Each place you slide the decimal to the left increase the exponent by 1
	- Each Place you slide the decimal to the right decreases the exponent by 1

- Trim off any leading zeros (on the left end of the significand) 
- Trim off any trailing zeros (on the right end of the significand) Only if the original number had no decimal point. We are assuming they aren't significant. If you have additional information to suggest they are you need to keep them. 
- Here are some examples

```
Start with: 600.410
Slide decimal left 2 spaces: 6.00410e2
No leading zeros to trim: 6.00410e2
Don't trim trailing zeros: 6.00410e2 (6 significant digits)
```



```
Start with: 0.0078900
Slide decimal right 3 spaces: 0007.8900e-3
Trim leading zeros: 7.8900e-3
Don't trim trailing zeros: 7.8900e-3 (5 significant digits)

Start with: 42030 (no information to suggest the trailing zero is significant)
Slide decimal left 4 spaces: 4.2030e4
No leading zeros to trim: 4.2030e4
Trim trailing zeros: 4.203e4 (4 significant digits)

Start with: 42030 (assuming the trailing zero is significant)
Slide decimal left 4 spaces: 4.2030e4
No leading zeros to trim: 4.2030e4
Keep trailing zeros: 4.2030e4 (5 significant digits)
```



Handling trailing zeros

Consider the case where we ask two lab assistants each to weigh the same apple. One returns and says the apple weighs 87.0 grams. The other returns and says the apple weighs 87.000 grams. Let’s assume the weighing is correct. In the former case, the actual weight of the apple could be anywhere between 86.950 and 87.049 grams. Maybe the scale was only precise to the nearest tenth of a gram. Or maybe our assistant rounded a bit. In the latter case, we are confident about the actual weight of the apple to a much higher degree (it actually weighs between 86.99950 and 87.00049 grams, which has much less variability).

When converting to scientific notation, trailing zeros after a decimal are considered significant, so we keep them:

- 87.0g = 8.70e1
- 87.000g = 8.7000e1

For numbers with no decimal point, trailing zeros are considered to be insignificant by default. Given the number 2100 (with no additional information), we assume the trailing 0s are not significant, so we drop them:

- 2100 = 2.1e3 (trailing zeros assumed not significant)

However, if we happened to know that this number was measured precisely (or that the actual number was somewhere between 2099.5 and 2100.5), then we should instead treat those zeros as significant:

- 2100 = 2.100e3 (trailing zeros known significant)

Tip

You may occasionally see a number written with a trailing decimal point. This is an indication that the preceding zeros are significant.

- 2100. = 2.100e3 (trailing zeros known significant)

One of the nice things about scientific notation is that it always makes clear how many digits are significant.

From a technical standpoint, the numbers 87.0 and 87.000 have the same value (and the same type). When C++ stores either of these numbers in memory, it will store just the value 87. And once stored, there is no way to determine from the stored value which of the two numbers was originally input.

Now that we’ve covered scientific notation, we’re ready to cover floating point numbers.




34.50
3.450e1



0.004000
4.000e-3



123.005

1.23005e2


146000
1.46e5



1.46000001e5





3.45000e4


1.46000e5