

the .reduce method reduces the elements of an array to a single value. Lets say we have an array of numbers that is the Cost of each item in a shopping cart, lets sum all of those numbers into one and return a total


const prices = [1,20,3,3,4]

  

const total = prices.reduce(sum);

  

console.log(total);

  

function sum(previouselement, element){

    return previouselement + element;

  

}

the previouselement is a accumulator, meaning it accumulates values.

const prices = [1,20,3,3,4,20,99,100,1]

  

const total = prices.reduce(max);

  

console.log(total);

  

function max(accumlator, element){

    return Math.max(accumlator, element);

  

}


this would give you the maximum value.



## [Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#syntax)

jsCopy to Clipboard

```
reduce(callbackFn)
reduce(callbackFn, initialValue)
```


the callbackFn is a function to execute for each element in the array its return value becomes the value of the accumulator parameter on the next invocation of callbackFn. For the last invocation, the return value becomes the return value of `reduce()`. The function is called with the following arguments:

[`accumulator`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#accumulator)

The value resulting from the previous call to `callbackFn`. On the first call, its value is `initialValue` if the latter is specified; otherwise its value is `array[0]`.


[`currentValue`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#currentvalue)

The value of the current element. On the first call, its value is `array[0]` if `initialValue` is specified; otherwise its value is `array[1]`.

[`currentIndex`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#currentindex)

The index position of `currentValue` in the array. On the first call, its value is `0` if `initialValue` is specified, otherwise `1`.

[`array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#array)

The array `reduce()` was called upon.


