---
layout: default
title: Array Callback Methods
parent: Intro to JavaScript
nav_order: 4
---
# Callback Methods
Many methods in JavaScript take as an argument a "callback" function which is called on some input; arrays make especially heavy use of these to apply various effects to all of the values inside the array.

## Iterative Methods
Most programs do iteration over iterables like arrays using some sort of `for` or `while` loop. JavaScript does have these structures; however, an alternative form of iteration is prefered, and the default linter settings used in Furman Now! avoid using these loops. Instead, we use functions on the array itself to simualte these behaviors. These functions are called 'Iterative Methods'

JavaScript has three main iterative methods - there are many more of them, but these three are the most commonly used. Each of these functions iterates over all of the elements of an array and produces some output on their basis.

### .map()
`.map()` is a method which takes each element in an array and "maps" it to a new value. Something like normalization of a range would be a classic example of a "mapping"; if we are trying to take our values from a range of `-25` to `192` to the range of `0` to `1`, we could map the array with these values in it. This will output a new array, called the 'mapping', which will have an output corresponding to each original entry, located at the same position in the array. 

`.map()` is applied to an array, and has as its argument an anonymous function which is applied to each element of the initial array. `.map()` will provide this function with up to three arguments as needed. The first is the element in the old array; the second is the element's index in the array; and the third is the full array, if needed. We almost never need more then the first argument, and on rare occasion the second argument. Anything that makes use of the third argument is almost always better pre-computed outside the `.map()`'s anonymous function.

```js
const arr = [119, -25, 152, 46, 98, 192, 16];
const [min, max] = [Math.min(...arr), Math.max(...arr)]
const normalized = arr.map( (entry) => (entry - min) / (max - min) );

console.log(normalized); // => [0.664, 0, 0.816, 0.327, 0.567, 1, 0.189]
// The first entry is the normalization of 119, the second the normalization of -25... etc.
```

### .filter() 

`.filter()` works similarly to `.map()`, but does not return a transformed list; instead, it outputs a new list that removes elements which do not meet some condition. The function provided to `.filter()` always returns either a `true` or a `false`, and only entries which return `true` are kept in the new array.

```js
const overFifty = arr.filter( (entry) => entry > 50)
console.log(overFifty) // => [119, 152, 98, 192]
```

This is incredibly valuable for removing entries in an array that do not meet some formatting, or are not above some threshold, or anything of the like.

### .forEach()

`.forEach()` is similar to `.map()` and `.filter()`, but it does not produce any output. Instead, it relies on 'side effects' to produce any change. `.forEach()` methods will usually rely on manipulating some high-scope value to produce an output; say, for instance, if we were printing each element of the array.

```js
arr.forEach((entry) => console.log(entry));
/*
 * 119
 * -25
 * 152
 * 46
 * 98
 * 192
 * 16
 */
```

## Semi-Iterative Methods
Some methods act like iterative methods, but differ from their basic format in some way. Two of these which are very important are `.reduce()` and `.sort()`.

### .reduce()
Reduce takes an array and "reduced" it down to a single value. Imagine attempting to sum a list, or create it's total product; `.reduce()` allows this to be done. `.reduce()` takes two arguments, a callback and an 'initial' value. The callback itself is provided two values: the current entry and the "accumulator," which is the output of the last callback. This last "accumulator" is returned at the end of the function. `.reduce()` begins with element index `[0]` and ends at the array's last element; there is an identical `.reduceRight()` which is formatted the same way as `.reduce()`, but applies reduction from the last element to the first instead.

```js
const sum = arr.reduce((entry, accum) => entry + accum, 0);
const prod = arr.reduce((entry, accum) => entry * accum, 1);

console.log(sum, prod); // => 598, -6262326067200
```

### .sort()
`.sort()` is used to order a list. Its callback is given two arguments, usually called `a` and `b`, which are two elements from the list, and is expected to return a "comparison" between the two. If `a` is greater than `b`, the function is expected to return a number greater than 0; if `b` is greater than `a`, the function should return a number less than 0; if `a` is equal to `b`, the function should return 0. This is simple enough with numbers; a comparison can simply be implemented as `a - b`, or (if you want to be nice and keep the outputs strictly as -1, 0, and 1) `(a > b) - (b > a)` (this works because `-` coerces `true` and `false` into 0 and 1, so if `a` is greater, `true - false` is `1 - 0`,  if `b` is greater, `false - true` is `0 - 1`, and if `a` equals `b`, `false - false` is `0 - 0`). This callback can integrate in more complex behavior as needed to correctly sort the list into the desired order.

```js
const sorted = arr.sort((a, b) => (a > b) - (b > a));
console.log(sorted); // => [-25, 16, 46, 98, 119, 152, 192]
```
